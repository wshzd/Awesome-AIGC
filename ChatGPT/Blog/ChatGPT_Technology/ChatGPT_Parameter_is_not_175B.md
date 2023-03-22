ChatGPT Parameter is not 175B

**原文链接**：https://orenleung.super.site/is-chatgpt-175-billion-parameters-technical-analysis

> OpenAI 推出的 ChatGPT 到底是不是 1750 亿参数的等价大模型呢？这篇文章或许能带给你答案。

ChatGPT 的火热持续到了今天，围绕它的爆点新闻和技术解读不断涌现。关于其参数量，有一种普遍的假设认为，ChatGPT 的参数量与 GPT-3 论文中介绍的 1750 亿参数模型相同。但是，深耕于大语言模型领域工作的人很清楚这不是真的。通过对 A100 GPU 的内存带宽分析，就会发现 ChatGPT API 的实际推理速度要比 1750 亿 Dense equivalent 模型的最大理论推理速度快很多。

本文将使用反证法来证明并支持上面的论点，只需要使用大学里学到的一些理论知识。另外需要注意，还存在相反的问题，即有人声称 ChatGPT 只有 X 亿个参数（X 远远低于 1750 ）。但是，这些说法无法得到验证，因为说这些话的人通常是道听途说。

接下来是详细的论证过程。

**反证法**

先假设 ChatGPT 模型有 1750 亿个参数，通常用 INT8 格式来存储 LLM 权重，以便进行更低延迟的推理、更高的吞吐量和更低的内存需求（比用 float16 格式来存储要少两倍的内存）。每个 INT8 参数需要 1 个字节进行存储。简单的计算就知道，模型需要 175GB 的存储空间。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9LmGUsXS5PpHNje4sW1GibSzP1xzMNGP4s3tL0gqLcB6XKS5TqZVPf1mX99jZsth5znbgQHPzcjMQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)*图片出自 INT8 SmoothQuant 论文，地址：https://arxiv.org/abs/2211.10438*

就推理而言，GPT 风格的语言模型在每次前向传递时都是「自回归」的，它预测下一个最可能的 token（对于类似 ChatGPT 的 RLHF 模型，它会预测其人类标注者更偏好的下一个 token）。这意味着要生成 200 个 token，因此需要执行 200 个前向传递。对于每个前向传递，我们需要将模型的所有权重从高带宽（HBM）内存加载到矩阵计算单元（GPU 的张量计算核）中， 也就是说需要为每个前向传递加载 175GB 的权重。

在微软 Azure 平台上，一个节点上可以分配 A100 的最大数量是 8。这意味着每个模型实例的最大张量并行度是 8。因此，其实不需要为每个前向传递加载 175GB 的权重，而只需要为每个前向传递的每个 GPU 加载 21.87GB，因为张量并行性可以在所有 GPU 上并行化权重和计算。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/KmXPKA19gW9LmGUsXS5PpHNje4sW1GibSvQEPwLFzsEibhvzo1l7Xdoicib61srQ4mibbVnstp8sic382uE1RdX3K2zw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)*图片出自 Megatron-LM 论文，地址：https://arxiv.org/abs/1909.08053*

在 A100 80GB SXM 版本上，最大内存带宽是 2TB/s。这意味着在 batchsize=1 的情况下（受内存带宽限制），前向传递最大的理论速度将达到 91 次 / 秒。同时，大部分时间都花在加载权重上，而不是计算矩阵乘法。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9LmGUsXS5PpHNje4sW1GibSam25d4yRelWseK3htiba2HYzgaia6Dch3RZKdUAunFecLTCRib89dJ1uw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)*注意：对于 fp16/bfloat16，当受内存带宽限制时，最大的理论前向传递速度达到 45.5 次 / 秒。*

**ChatGPT 的实际延迟是多少？**

在夜间运行 Python 编写的脚本（夜间运行的开销更低），来测试通过 OpenAI API 使用 ChatGPT 的延迟，前向传递能够获得的最大实证速度是 101 次 / 秒。本文使用了实验的最大实证结果，这是因为需要从 OpenAI 的后端和动态批处理系统获得最低开销。

**结论**

根据前面假设和论证，我们可以发现存在矛盾的地方，因为基于实证的结果比基于 A100 平台内存带宽的最大理论结果要快得多。因此可以得出结论，OpenAI 用于推理的 ChatGPT 模型绝对不是等价于 1750 亿参数的稠密模型。

**常见问题问答**

**1、为什么预测 ChatGPT 推理模型的参数量而不是训练模型的参数量？**

使用内存带宽方法来估计模型参数数量，这只适用于推理模型。我们无法确切地知道 OpenAI 是否应用了蒸馏等技术，使其推理模型比训练模型更小。

> 许多昆虫都有一种幼虫形态，其在从环境中提取能量和营养方面进行了优化，而完全不同的成体形态则在旅行和繁殖的非常不同的要求方面进行了优化。—— 出自 Geoffrey Hinton、Oriol Vinyals、Jeff Dean，2015 年。

**2、是否有做其它的假设？**

证明中其实还包括 3 个假设：

- 假设计算巨大矩阵乘法所需的时间相对于每个前向传递加载参数的时间为 0；
- 假设进行 GPU 之间的通信所需的时间也为 0。如果不假设 GPU 之间的通信和矩阵乘法所需的时间为 0，则 1750 亿参数模型的每秒最大理论 token 将会减少；
- 假设 ChatGPT 是基于 Transformer 架构的变种。

**3、Dense Equivalent 是什么意思？**

过去几年中，研究人员已经进行关于稀疏混合专家 LLM（如 Switch Transformer）的研究。Dense equivalent 表示每次前向传递使用多少参数。使用本文所述的方法，无法证明 ChatGPT 不是一个 1750 亿参数的稀疏 MoE 模型。

**4、是否考虑过 KV 缓存 Transformer 推理优化？**

就算使用 KV 缓存优化，每次前向传递仍需要加载整个模型，KV 缓存仅在 FLOPs 上节省，但不会减少内存带宽消耗（实际上它会增加，因为需要每次前向传递都加载 KV 缓存）。

**5、是否考虑过 Flash Attention？**

虽然 Flash Attention 在内存带宽效率和实际时间速度方面表现更好，但每次前向传递仍需要加载整个模型，因此前面的论证仍然成立。

**6、是否考虑过管道并行 / 更细粒度的并行策略？**

利用 pipeline 并行会导致相同的最大前向传递次数。但是，通过使用 micro-batch 和更大的 batch 大小，吞吐量（总 token 数 / 秒）可以增加。

**7、考虑过将张量并行性增加到 8 以上吗？**

A100 平台支持每个节点 16 个 A100，但 Azure 不支持此功能。只有 Google Cloud 支持此功能，但几乎没有人使用。Azure 不太可能为 OpenAI 定制一个带有 16 个 A100 的节点，并且不将其发布为公共 GA 版本，以分摊设计或维护新节点的成本。关于节点间的张量并行性，这只是一个可能性，但这是一种不太具成本效益的在 A100 上进行推理的方式。就连英伟达也不建议对节点间的张量并行处理。

**8、有没有考虑使用 INT4 存储权重？**

尽管使用 INT4 被证明有效，但是 OpenAI 的 GPU Kernel Compiler 不支持 INT4 的加载、存储或矩阵乘法，也没有计划将 INT 加入到他们的技术路线图中。由于不支持 INT4 的加载或存储，你甚至无法像将权重存储为 INT4，然后量化转回高精度格式（如 INT8、bfloat16 等）。

参考链接：

- *htt**ps://kipp.ly/blog/transformer-inference-arithmetic/*
- *https://www.nvidia.com/content/dam/en-zz/Solutions/Data-Center/a100/pdf/nvidia-a100-datasheet-us-nvidia-1758950-r4-web.pdf*
- *https://openai.com/research/techniques-for-training-large-neural-networks*
- *https://arxiv.org/abs/2211.10438*
- *https://arxiv.org/abs/1909.08053*
- *https://arxiv.org/abs/2005.14165*