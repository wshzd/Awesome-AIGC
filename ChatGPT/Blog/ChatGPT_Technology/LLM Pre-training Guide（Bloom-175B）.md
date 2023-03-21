# LLM Pre-training Guide（Bloom-175B）

近年来，训练越来越大的语言模型已成为常态（悟道 2.0 模型参数量已经到达 1.75T ，为 GPT-3 的 10 倍）。但如何训练大型语言模型的信息却很少查到 。

通过查找，这里整理了简单的训练指南

> 以 BLOOM-175B 的训练为例

## **1. 概况**

### **1.1 硬件设施**

这里为 BLOOM 的训练使用的硬件设施，可以参考

- GPUs: 384 张 NVIDIA A100 80GB GPUs (48 个节点，单个节点 8 张卡) + 32 张备用 GPU
- 每个节点 8 个 GPU 使用 NVLink 4 inter-gpu connects，4 OmniPath links
- CPU: AMD EPYC 7543 32-Core Processor
- CPU memory: 每个节点 512GB
- GPU memory: 每个节点 640GB
- 节点间连接: Omni-Path Architecture (OPA) w/ non-blocking fat tree
- NCCL-communications network: a fully dedicated subnet
- 硬盘 IO 网络: IBM 通用并行文件系统-GPFS shared with other nodes and users

### **1.2 Checkpoints**

- 包括 fp32 优化器状态和 bf16+fp32 权重的 Checkpoints 为 2.3TB
- 只有 bf16 权重的 Checkpoints 为 329GB

## **2. 模型训练**

### **2.1 Megatron-DeepSpeed**

> 176B BLOOM 模型使用 Megatron-DeepSpeed 进行训练。

Megatron-DeepSpeed 结合了两种主要技术：

- DeepSpeed 是一个深度学习优化库，它使分布式训练变得简单、高效和有效。
- Megatron-LM 是由 NVIDIA 的应用深度学习研究团队开发的大型、强大的 Transformer 模型框架。

DeepSpeed 团队通过将 DeepSpeed 库中的 **ZeRO 分片（ZeRO sharding）和管道并行（pipeline parallelism）与 Megatron-LM 中的张量并行（Tensor Parallelism）相结合，开发了一种基于 3D 并行的实现**。下文会更为详细介绍这些技术。

Megatron-DeepSpeed 实施 3D 并行以可以让大型模型以非常有效的方式进行训练。。

- **DataParallel (DP)** - 相同的初始化模型被复制多次，并且每次都被馈送 minibatch 的一部分。处理是并行完成的，所有设置在每个训练步骤结束时进行同步。
- **TensorParallel (TP)** - 每个张量都被分成多个块，因此不是让整个张量驻留在单个 GPU 上，而是张量的每个分片都驻留在其指定的 GPU 上。在处理过程中，每个分片在不同的 GPU 上分别并行处理，最终结果在步骤结束时同步。这也被称作横向并行。
- **PipelineParallel (PP)** - 模型在多个 GPU 上垂直（层级）拆分，因此只有模型的一个或多个层放置在单个 GPU 上。每个 GPU 并行处理管道的不同阶段，并处理一小部分批处理。
- **零冗余优化器 (ZeRO)** - 也执行与 TP 有点类似的张量分片，除了整个张量会及时重建以进行前向或反向计算，因此不需要修改模型。它还支持各种卸载技术以补偿有限的 GPU 内存。

### **2.2 数据并行**

分布式训练最常见的就是 DistributedDataParallel (DDP) PyTorch 文档。在这种方法中，模型被完全复制到每个 GPU，然后在每次迭代后所有模型相互同步它们的状态。这种方法可以加快训练速度，但只有当模型可以适合单个 GPU 时，它才有效。

我们以经典的手写数字识别为例：

![img](https://pic4.zhimg.com/80/v2-b508d84ba9c6a9c6ae2c5be70526da43_720w.webp)

数据并行通过在 N 台机器上复制模型来实现。拆分 minibatch ，分成 N 个块，让每台机器处理一个块。

![img](https://pic3.zhimg.com/80/v2-678f7d2c116f7528be27d6445b6c091a_720w.webp)

通过跨多个节点拆分，每个节点要做的工作更少，而且，如果忽略通信开销，上图的训练速度应该快 2 倍。Batch 中的样本可以独立处理。（但值得注意 Batchnorm 等其他算子）因此，在前向传播（计算每个样本的输出）和反向传播（计算单个样本损失权重的梯度）期间不需要通信。

为了实现顺序一致性（**生成的梯度与在单台机器上使用顺序训练计算出的梯度相同**）。需要在更新权重之前同步梯度。最常用的损失函数是单个样本损失的均值：

loss(batch)=1N∑i=0batchsizeloss(inputi,targeti)

为了计算更方便，最终梯度是每个项的梯度的总和。因此，可以在每台机器上独立计算样本的梯度，并在执行权重更新之前将它们相加。

∇Wsync′d=1#Nodes∑i=0#Nodes∇Wilocal

> 值得注意的是如果使用随机梯度下降（SGD），同步权重和同步梯度是一样的：
> 1N∑i(W+λ∇Wi)=W+λN∑i∇Wi**但是，这不适用于像 Adam 这样的有状态优化器**，因为更新状态是梯度的非线性函数。如果使用 Adam 并同步权重而不是梯度，则每个节点上的优化器状态都会发生分歧，并且会失去顺序一致性。

### **2.2.1 ZeRO 数据并行**

详细内容可以参考：[https://www.microsoft.com/en-us/research/blog/zero-deepspeed-new-system-optimizations-enable-training-models-with-over-100-billion-parameters/](https://link.zhihu.com/?target=https%3A//www.microsoft.com/en-us/research/blog/zero-deepspeed-new-system-optimizations-enable-training-models-with-over-100-billion-parameters/)

![img](https://pic1.zhimg.com/80/v2-b5548a391adf3b983876ce94a0be83ac_720w.webp)

ZeRO 具有三个主要的优化阶段，它们对应于优化器状态（optimizer states）、梯度（gradients）和参数（parameters）的划分。累积启用时：

1. 优化器状态分区 (Pos) – 内存减少 4 倍，通信量与数据并行性相同
2. 添加梯度分区 (Pos+g) – 内存减少 8 倍，通信量与数据并行性相同
3. 添加参数分区 (Pos+g+p) – 内存减少与数据并行度 Nd 成线性关系。例如，拆分为 64 个 GPU (Nd=64) 内存将减少到 1/64 。GPU 通信量略有增加 50%。

> ZeRO 消除了显存冗余并使集群显存容量可用。启用所有三个阶段后，ZeRO 可以仅在 1024 个 NVIDIA GPU 上训练万亿参数模型。例如像 Adam 这样的 16 位精度优化器的万亿参数模型需要大约 16 TB 的内存来保存优化器状态、梯度和参数。 16TB 除以 1024 就是 16GB，这对于 GPU 来说是一个合理的范围。

### **2.3 张量并行**

Megatron-LM 论文：[https://arxiv.org/abs/2104.04473](https://link.zhihu.com/?target=https%3A//arxiv.org/abs/2104.04473)

在 Tensor Parallelism (TP) 中，每个 GPU 仅处理张量的一部分，并且仅聚合完整的张量以用于需要整个事物的操作。 这里使用 Megatron-LM 论文中的实现：GPU 集群上的高效大规模语言模型训练。 任何 Transformer 的主要构建块都是一个完全连接的 `nn.Linear`，然后是一个非线性激活 GeLU。 按照 Megatron 论文的符号，可以将其点积部分写为Y=GeLU(XA)，其中 `X` 和 `Y` 是输入和输出向量，`A` 是权重矩阵。 如果以矩阵形式查看计算，很容易看出矩阵乘法如何在多个 GPU 之间拆分：

![img](https://pic4.zhimg.com/80/v2-ad9ba269a2752f2af36bfbcafc2f8ce7_720w.webp)

如果我们将权重矩阵 `A` 按列拆分到 N 个 GPU 上并并行执行矩阵乘法 XA1 到 XAn，那么最终将得到 N 个输出向量、、、Y1、Y2、...、Yn，它们可以独立地输入到 GeLU：

[Y1,Y2]=[GeLU(XA1),GeLU(XA2)]

> 注意 Y 矩阵沿列拆分，我们可以沿其行拆分第二个 GEMM，这样它就可以直接获取 GeLU 的输出，而无需任何额外的通信。

使用这个原理，可以更新任意深度的 MLP，同时在每个行列序列之后同步 GPU。 Megatron-LM 论文为此提供了一个有用的说明：

![img](https://pic4.zhimg.com/80/v2-8c0983e3cb19940bcd05ee4c2275cbaf_720w.webp)

其中 `f` 是前向传播中的恒等运算符，在反向传播中是 `all-reduce`，而 `g` 是前向传播中的 `all-reduce` 和反向传播中的恒等运算符。 并行化多头注意力层甚至更简单，因为它们本来就是并行的

![img](https://pic3.zhimg.com/80/v2-1a3ada517a94ac7be982533c75e219fe_720w.webp)

特殊考虑：由于前向和后向传播中每层都有两个 `all-reduce`，因此 TP 需要在设备之间进行非常快速的互连。因此，除非有一个非常快的网络，否则**不建议跨多个节点进行 TP**。

> 在 BLOOM 的例子中，节点间通信比 PCIe 慢得多。实际上，如果节点有 4 个 GPU，则最高 TP 度因此为 4。如果需要 TP 度为 8，则需要使用至少有 8 个 GPU 的节点。 该组件由 Megatron-LM 实现。 Megatron-LM 最近扩展了张量并行性，以包括序列并行性，它沿着序列维度拆分不能像上面那样拆分的操作，例如 LayerNorm。论文 Reducing Activation Recomputation in Large Transformer Models 提供了此技术的详细信息

### **2.4 管道并行**

朴素流水线并行（Naive Pipeline Parallelism）是将一组模型层分布在多个 GPU 上，并简单地将数据从 GPU 移动到 GPU，就好像它是一个大型复合 GPU 一样。该机制相对简单 - 切换所需的层 `.to()` 所需的设备，现在只要数据进出这些层，就会将数据切换到与该层相同的设备，其余部分保持不变。 这显示了纵向模型并行性，会垂直切片 layers。例如，如果下图显示一个 8 层模型：

```
===================  ===================
|  0 | 1 | 2 | 3  |  |  4 | 5 | 6 | 7  |
===================  ===================
        GPU0                 GPU1
```

只是将它垂直分成 2 部分，将层 0-3 放置在 GPU0 上，将层 4-7 放置在 GPU1 上。

现在，当数据从第 0 层到第 1 层、第 1 层到第 2 层和第 2 层到第 3 层传输时，这就像单个 GPU 上普通模型的前向传递。但是当数据需要从第 3 层传递到第 4 层时，它需要从 GPU0 传递到 GPU1，**这会引入通信开销**。如果参与的 GPU 位于同一计算节点（例如同一台物理机器）上，则此复制非常快，但如果 GPU 位于不同的计算节点（例如多台机器）上，通信开销可能会大得多。 然后第 4 到 5 到 6 到 7 层就像普通模型一样，当第 7 层完成时，我们通常需要将数据发送回标签所在的第 0 层（或者将标签发送到最后一层）。现在可以计算损失并且优化器可以完成它的工作。

问题：

- 之所以这个被称为朴素流水线并行，因为其存在缺陷：**是除了一个 GPU 之外的所有 GPU 在任何给定时刻都是空闲的**。因此，如果使用 4 个 GPU，则几乎等同于将单个 GPU 的内存量翻两番，而忽略其余硬件。另外还有在设备之间复制数据的开销。所以 4x 6GB 卡将能够容纳与使用朴素流水线并行的 1x 24GB 卡相同大小的模型训练，但后者将更快地完成训练，因为它没有数据复制开销。
- 共享嵌入可能需要在 GPU 之间来回复制。

流水线并行 (PP) 与上述朴素流水线并行几乎相同，但它解决了 GPU 闲置问题，方法是将传入的 batch 为 micro-batches 并人工创建流水线，从而允许不同的 GPU 同时参与计算过程。 GPipe 论文（[https://ai.googleblog.com/2019/03/introducing-gpipe-open-source-library.html](https://link.zhihu.com/?target=https%3A//ai.googleblog.com/2019/03/introducing-gpipe-open-source-library.html)）中的下图显示了两者差别：

![img](https://pic2.zhimg.com/80/v2-a70604fea85190050549999e7a70d6f5_720w.webp)

从图表中很容易看出第二种方式的空白区域（GPU 处于空闲状态）更少。空白部分称为“气泡”。 **该图的两个部分都显示了 4 度的并行性**。即 4 个 GPU 参与管道。于是就有了 F0、F1、F2、F3 这 4 个管道的正向路径，然后是 B3、B2、B1、B0 的返回逆序反向路径。 **PP 引入了一个新的超参数来调整，称为块**。它定义了通过同一管道阶段按顺序发送多少数据块。例如，在底部图表中，可以看到 `chunks=4`。 GPU0 在块 0、1、2 和 3（F0,0、F0,1、F0,2、F0,3）上执行相同的前向路径，然后等待其他 GPU 完成它们的工作，只有当他们的工作开始完成时，GPU0 才开始重新工作，做 3、2、1 和 0 块的后向路径（B0,3, B0,2, B0,1, B0,0）

> 请注意，从概念上讲，这与梯度累积步骤 (GAS) 的概念相同。 PyTorch 使用 chunks，而 DeepSpeed 指的是与 GAS 相同的超参数。

因为块，PP 引入了 micro-batches（MBS）的概念。 DP 将全局数据批量大小拆分为小批量，因此如果 DP 度为 4，则 global data batch size 1024 将拆分为 4 个 mini-batches，每个 mini-batches 256 (1024/4)。如果块（或 GAS）的数量为 32，最终得到的 micro-batches 大小为 8（256/32）。每个流水线阶段一次处理一个 micro-batches。

> 为了计算 DP + PP 设置的 global data batch size，执行：$$mbs*chunks*dp_{degree} (8*32*4=1024)$$。

使用 `chunks=1` 你最终会得到非常低效的朴素管道并行。**如果块值非常大，您最终会得到很小的 micro-batches 大小，这也可能不是很有效**。因此，必须通过实验来找到导致 GPU 最有效利用的值。 虽然该图显示存在无法并行化的空白时间气泡，因为最后一个前向阶段必须等待后向完成管道，但为块找到最佳值的目的是**实现高并发所有参与 GPU 的 GPU 利用率，这转化为最小化气泡的大小**。 这种调度机制被称为 *all forward all backward*。 虽然 Megatron-LM 和 DeepSpeed 都有自己的 PP 协议实现，但 Megatron-DeepSpeed 使用 DeepSpeed 实现，因为它与 DeepSpeed 的其他方面集成在一起。

> 在 bloom 实践中:
> 这里的另一个重要问题是 word embedding 矩阵的大小。虽然通常 word embedding 矩阵比 transformer block 消耗更少的内存，但在有 250k 词汇表的情况下， word embedding 层需要 7.2GB 的 bf16 权重，而 transformer block 仅为 4.9GB。因此，不得不指示 Megatron-Deepspeed 将 word embedding 层视为一个 transformer block。所以有一个 72 层的管道，其中 2 个专门用于 embedding（第一个和最后一个）。这允许平衡 GPU 内存消耗。如果不这样做，我们就会让第一阶段和最后阶段消耗大部分 GPU 内存，而 95% 的 GPU 将使用更少的内存，因此训练将远非高效。

### **2.5 DP+PP**

DeepSpeed 教程（[https://www.deepspeed.ai/tutorials/pipeline/](https://link.zhihu.com/?target=https%3A//www.deepspeed.ai/tutorials/pipeline/)）中的下图演示了如何将 DP 与 PP 结合起来。

![img](https://pic1.zhimg.com/80/v2-127d807df8f6efc7b1f8cb6d5ff38620_720w.webp)

这里重要的是要了解 DP Rank 0 如何看不到 GPU2 (和普通 DP 一样)以及 DP Rank 1 如何看不到 GPU3。对于 DP，只有 GPU 0 和 1，它在其中提供数据，就像只有 2 个 GPU 一样。 GPU0 使用 PP ”透明地“将它的一些负载卸载到 GPU2。 GPU1 通过使用 GPU3 的帮助来做同样的事情。篇幅限制就不展示了。 由于每个维度至少需要 2 个 GPU，因此在这里至少需要 4 个 GPU。

### **2.6 DP+PP+TP**

为了获得更高效的训练，PP 与 TP 和 DP 相结合，称为 3D 并行性。这可以在下图中看到。

![img](https://pic1.zhimg.com/80/v2-7951815d9ab95beedf1d238bc58e73f0_720w.webp)

可以参考：[https://www.microsoft.com/en-us/research/blog/deepspeed-extreme-scale-model-training-for-everyone/](https://link.zhihu.com/?target=https%3A//www.microsoft.com/en-us/research/blog/deepspeed-extreme-scale-model-training-for-everyone/)

> 由于每个维度至少需要 2 个 GPU，因此在这里至少需要 8 个 GPU 才能实现完整的 3D 并行性。

### **2.7 ZeRO DP+PP+TP**

DeepSpeed 的主要功能之一是 ZeRO，它是 DP 的超级可扩展扩展。 ZeRO Data Parallelism 中已经在前文讨论过了。通常它是一个独立的功能，不需要 PP 或 TP。但可以与PP、TP结合使用。 当 ZeRO-DP 与 PP（和可选的 TP）结合时，它通常只启用 ZeRO 阶段 1，它只对优化器状态进行分片。 ZeRO 第 2 阶段还对梯度进行分片，第 3 阶段也对模型权重进行分片。 虽然理论上可以将 ZeRO 第 2 阶段与 Pipeline Parallelism 一起使用，但它会对性能产生不良影响。每个 micro-batches 都需要一个额外的 reduce-scatter 集合来在分片之前聚合梯度，这会增加潜在的显着通信开销。根据流水线并行性的性质，使用小的 micro-batches，重点是尝试平衡计算强度（ micro-batches 大小）与最小化流水线气泡（micro-batches 的数量）。因此，这些通信成本将会显著增加。 **此外，由于 PP，层数已经比正常情况下少，因此内存节省不会很大。 PP 已经将梯度大小减少了 1/PP，因此在此之上的梯度分片节省不如纯 DP 显著。** ZeRO 第 3 阶段也可用于训练这种规模的模型，但是，它需要比 DeepSpeed 3D 并行实现更多的通信。

### **2.8 BF16Optimizer**

![img](https://pic4.zhimg.com/80/v2-f16eec03db8842daf0d588efaef69a9f_720w.webp)

在 FP16 中训练巨大的 LLM 模型是一个禁忌（在 FP16 训练会导致数值不稳定，或者不能产生足够的精度使模型正确收敛 ）。

> BLOOM 训练报告中也指出了 FP16 loss 不稳定的问题

![img](https://pic1.zhimg.com/80/v2-f152a3ff2431fc795a54fc830f2ec578_720w.webp)

BF16 格式的关键是具有与 FP32 相同的指数位，因此不会与 FP16 一样容易溢出，使用最大数值范围为 64k 的 **FP16，只能乘以小范围的数**。例如可以做 `250*250=62500`，但如果你尝试 `255*255=65025`，结果就会溢出，这是导致训练期间出现主要问题的原因。这意味着你的权重必须保持很小。一种称为损失缩放的技术可以帮助解决这个问题，但是当模型变得非常大时，FP16 的有限范围仍然是一个问题。 **BF16 就没有这个问题**，可以轻松做到 `10 000*10 000=100 000 000` 当然，由于 BF16 和 FP16 的大小相同，均为 2 个字节，因此，当使用 BF16 时，它的劣势也会暴露：精度非常差。 无论使用 BF16 还是 FP16，都有一个权重副本始终在 FP32 中——这是由优化器更新的内容。**因此 16 位格式仅用于计算，优化器以全精度 FP32 更新权重，然后将它们转换为 16 位格式以用于下一次迭代**。

一个关键问题是梯度累积，它是管道并行性的主要特征之一，因为每个 micro-batches 的梯度都会累积。在 FP32 中实现梯度累积以保持训练的精确性至关重要，这就是 BF16Optimizer 所做的。

实践中，除了其他改进之外，BLOOM 团队认为使用 BF16 混合精度训练将潜在的噩梦变成了一个相对平稳的过程，这可以从以下 lm 损失图中观察到：

![img](https://pic1.zhimg.com/80/v2-c837cde0c7c6a0086b7ee89f697db754_720w.webp)

## **3. NCCL**

![img](https://pic1.zhimg.com/80/v2-d32c46a261463e1ba5caef6b5e0fe6d0_720w.webp)

NCCL 全称 Nvidia Collective multi-GPU Communication Library ，是一个实现多 GPU 的collective communication 通信（all-gather, reduce, broadcast)库，Nvidia 做了很多优化，可以在 PCIe、Nvlink、InfiniBand 上实现较高的通信速度。

NCCL 具有以下技术特性：

- 高性能：NCCL 方便地消除了开发人员针对特定机器优化应用程序的需要。 NCCL 在节点内和跨节点的多个 GPU 上提供快速集合。
- 易于编程：NCCL 使用一个简单的 C API，可以很容易地从各种编程语言中访问。NCCL 紧跟由 MPI（消息传递接口）定义的流行的集合 API。
- 兼容性：NCCL 几乎与任何多 GPU 并行化模型兼容，例如：单线程、多线程（每个 GPU 使用一个线程）和多进程（MPI 与 GPU 上的多线程操作相结合）。

### **3.1. NCCL 特点**

下面分别从以下几个方面来介绍 NCCL 的特点，包括基本的 communication primitive、ring-base collectives、NCCL 在单机多卡上以及多机多卡实现

### **3.2 Communication Primitive**

并行任务的通信一般可以分为 Point-to-point communication 和 Collective communication 。P2P 通信这种模式只有一个 sender 和一个 receiver，实现起来比较简单。 第二种 Collective communication 包含多个 sender 多个 receiver，一般的通信原语包括 broadcast，gather,all-gather,scatter,reduce,all-reduce,reduce-scatter,all-to-all 等。简单介绍几个常用的操作：

- Reduce：从多个 sender 那里接收数据，最终 combine 到一个节点上

![img](https://pic2.zhimg.com/80/v2-fe26ffda0f48c40b3f4a8feb7a73a669_720w.webp)

- All-reduce：从多个 sender 那里接收数据，最终 combine 到每一个节点上

![img](https://pic3.zhimg.com/80/v2-42844fc757ab01338f110622f0bb4962_720w.webp)

而传统 Collective communication 假设通信节点组成的 topology 是一颗 fat tree，如下图所示，这样通信效率最高。但实际的通信 topology 可能比较复杂，并不是一个 fat tree。因此一般用 ring-based Collective communication。

![img](https://pic4.zhimg.com/80/v2-37413835247c9a2763e1286e2af7d02f_720w.webp)

### **3.3 Ring-base Collectives**

ring-base collectives 将所有的通信节点通过首尾连接形成一个单向环，数据在环上依次传输。以 broadcast 为例， 假设有 4 个 GPU，GPU0 为 sender 将信息发送给剩下的 GPU，按照环的方式依次传输，GPU0-->GPU1-->GPU2-->GPU3，若数据量为 N，带宽为 B，整个传输时间为(K−1)N/B。时间随着节点数线性增长，不是很高效。

![img](https://pic2.zhimg.com/80/v2-12af80e172e09cc92e4e6dcde6841311_720w.webp)

下面把要传输的数据分成 S 份，每次只传 N/S 的数据量，传输过程如下所示：

![img](https://pic4.zhimg.com/80/v2-fed2f439627bc1c16bec63cc7ec84cdf_720w.webp)

GPU1 接收到 GPU0 的一份数据后，也接着传到环的下个节点，这样以此类推，最后花的时间为

S∗(N/S/B)+(k−2)∗(N/S/B)=N(S+K−2)/(SB)→N/B

，条件是 S 远大于 K，即数据的份数大于节点数，这个很容易满足。所以通信时间不随节点数的增加而增加，只和数据总量以及带宽有关。其它通信操作比如 reduce、gather 以此类推。 那么在以GPU为通信节点的场景下，怎么构建通信环呢？如下图所示： 单机 4 卡通过同一个 PCIe switch 挂载在一棵CPU的场景：

![img](https://pic4.zhimg.com/80/v2-dac47e37dedf4ce07c92861c138b91e7_720w.webp)

单机 8 卡通过两个 CPU 下不同的 PCIe switch 挂载的场景：

![img](https://pic4.zhimg.com/80/v2-1400c6742580fabed45eb4d02553df83_720w.webp)

### **3.4 NCCL 实现**

NCCL 实现成 CUDA C++ kernels，包含 3 种 primitive operations：Copy，Reduce，ReduceAndCopy。NCCL 1.0 版本只支持单机多卡，卡之间通过 PCIe、NVlink、GPU Direct P2P来通信。NCCL 2.0 会支持多机多卡，多机间通过 Sockets (Ethernet) 或者 InfiniBand with GPU Direct RDMA 通信。 下图所示，单机内多卡通过 PCIe 以及 CPU socket 通信，多机通过 InfiniBand 通信。

![img](https://pic4.zhimg.com/80/v2-c3c96eff75e8f1b161b6c62188370ea7_720w.webp)

同样，在多机多卡内部，也要构成一个通信环

![img](https://pic2.zhimg.com/80/v2-5614a5e2da87f34b0b76eabe40339f35_720w.webp)

下面是单机 4卡（Maxwel GPU）上各个操作随着通信量增加的带宽速度变化，可以看到带宽上限能达到10GB/s，接近PCIe的带宽。

![img](https://pic1.zhimg.com/80/v2-65f4fb71798f71c2663c369329d8a058_720w.webp)

下图是 Allreduce 在单机不同架构下的速度比较：

![img](https://pic2.zhimg.com/80/v2-155b290bdc2964e129d24fadc5784f8d_720w.webp)

先不看 DGX-1 架构，这是 Nvidia 推出的深度学习平台，带宽能达到 60GB/s 。前面三个是单机多卡典型的三种连接方式，第三种是四张卡都在一个 PCIe switch 上，所以带宽较高，能达到 >10GB/s PCIe 的带宽大小，第二种是两个 GPU 通过 switch 相连后再经过 CPU 连接，速度会稍微低一点，第一种是两个 GPU 通过 CPU 然后通过 QPI 和另一个 CPU 上的两块卡相连，因此速度最慢，但也能达到 >5GB/s。 下图是 Allreduce 多机下的速度表现，左图两机 8 卡，机内 PCIe ，机间 InfiniBand 能达到 >10GB/s 的速度，InfiniBand 基本上能达到机内的通信速度。

![img](https://pic3.zhimg.com/80/v2-7b912f62b04ea7c1853fb4c1ae037b46_720w.webp)

下图是 NCCL 在 CNTK ResNet50上的 scalability，32 卡基本能达到线性加速比。

![img](https://pic1.zhimg.com/80/v2-b12bcc3d8b0a89abb5403cd24e0009a0_720w.webp)

## **参考资料**

- [https://huggingface.co/blog/bloom-megatron-deepspeed](https://link.zhihu.com/?target=https%3A//huggingface.co/blog/bloom-megatron-deepspeed)
- [https://siboehm.com/articles/22/data-parallel-training](https://link.zhihu.com/?target=https%3A//siboehm.com/articles/22/data-parallel-training)
- [https://www.microsoft.com/en-us/research/blog/deepspeed-extreme-scale-model-training-for-everyone/](https://link.zhihu.com/?target=https%3A//www.microsoft.com/en-us/research/blog/deepspeed-extreme-scale-model-training-for-everyone/)
- [https://docs.nvidia.com/deeplearning/nccl/user-guide/docs/overview.html](https://link.zhihu.com/?target=https%3A//docs.nvidia.com/deeplearning/nccl/user-guide/docs/overview.html)
- [https://cloud.google.com/tpu/do](https://link.zhihu.com/?target=https%3A//cloud.google.com/tpu/docs/bfloat16%3Fhl%3Dzh-cn)