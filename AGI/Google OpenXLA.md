# Google OpenXLA



在去年 10 月的 Google Cloud Next 2022 活动中，OpenXLA 项目正式浮出水面，谷歌与包括阿里巴巴、AMD、Arm、亚马逊、英特尔、英伟达等科技公司推动的开源 AI 框架合作，致力于汇集不同机器学习框架，让机器学习开发人员获得能主动选择框架、硬件的能力。

本周三，谷歌宣布 OpenXLA 项目正式开源。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9XnWoRbEQaayhrJicumwd46pI4icrvOeqBNrwmWfMpIxQZLsb9QYUxLUXqDf8GCgzE5QhhT20pUib4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

项目链接：https://github.com/openxla/xla

通过创建与多种不同机器学习框架、硬件平台共同工作的统一机器学习编译器，OpenXLA 可以加速机器学习应用的交付并提供更大的代码可移植性。对于 AI 研究和应用来说，这是一个意义重大的项目，Jeff Dean 也在社交网络上进行了宣传。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWicQprCK8NjAfWYMCVWsKqiagJxyGjDxvkr94NFlATYCxYsV4qIIh9EPU4GV2CFj73T4hqwjjcAb7Nw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如今，机器学习开发和部署受到碎片化的基础设施的影响，这些基础设施可能因框架、硬件和用例而异。这种相互隔绝限制了开发人员的工作速度，并对模型的可移植性、效率和生产化造成了障碍。

3 月 8 日，谷歌等机构通过 OpenXLA 项目（其中包括 XLA、StableHLO 和 IREE 存储库）的开放，朝着消除这些障碍迈出了重要一步。

OpenXLA 是由 AI / 机器学习行业领导者共同开发的开源 ML 编译器生态系统，贡献者包括阿里巴巴、AWS、AMD、苹果、Arm、Cerebras、谷歌、Graphcore、Hugging Face、英特尔、Meta 和英伟达。它使得开发人员能够编译和优化来自所有领先机器学习框架的模型，以便在各种硬件上进行高效训练和服务。使用 OpenXLA 的开发人员可以观察到训练时间、吞吐量、服务延迟以及最终发布和计算成本方面的明显提升。

**机器学习技术设施面临的挑战**

随着 AI 技术进入实用阶段，许多行业的开发团队都在使用机器学习来应对现实世界的挑战，例如进行疾病的预测和预防、个性化学习体验和黑洞物理学探索。

随着模型参数数量呈指数级增长，深度学习模型所需的计算量每六个月翻一番，开发人员正在寻求基础架构的最大性能和利用率。大量团队正在利用多型号种类的硬件，从数据中心中的节能机器学习专用 ASIC 到可以提供更快响应速度的 AI 边缘处理器。相应的，为了提高效率，这些硬件设备使用定制化的独特算法和软件库。

但另一方面，如果没有通用的编译器将不同硬件设备桥接到当今使用的多种框架（例如 TensorFlow、PyTorch）上，人们就需要付出大量努力才能有效地运行机器学习。在实际工作中，开发人员必须手动优化每个硬件目标的模型操作。这意味着使用定制软件库或编写特定于设备的代码需要领域专业知识。

这是一个矛盾的结果，为了提高效率使用专用技术，结果却是跨框架和硬件的孤立、不可概括的路径导致维护成本高，进而导致供应商锁定，减缓了机器学习开发的进度。

**解决方法和目标**

OpenXLA 项目提供了最先进的 ML 编译器，可以在 ML 基础设施的复杂性中进行扩展。它的核心支柱是性能、可扩展性、可移植性、灵活性和易用性。借助 OpenXLA，我们渴望通过加速人工智能的开发和交付来实现 AI 在现实世界中的更大潜力。

OpenXLA 的目标在于：

- 通过适用于任何框架，接入专用设备后端和优化的统一编译器 API，使开发人员可以轻松地在他们的首选框架中针对各种硬件编译和优化任何模型。
- 为当前和新兴模型提供行业领先的性能，也可扩展至多个主机和加速器满足边缘部署的限制，并推广到未来的新型模型架构上。
- 构建一个分层和可扩展的机器学习编译器平台，为开发人员提供基于 MLIR 的组件，这些组件可针对其独特的用例进行重新配置，用于硬件定制化编译流程。

**AI/ML 领导者社区**

我们今天在机器学习基础架构中面临的挑战是巨大的，没有任何一个组织可以单独有效地解决这些挑战。OpenXLA 社区汇集了在 AI 堆栈的不同级别（从框架到编译器、runtime 和芯片）上运行的开发人员和行业领导者，因此非常适合解决我们在 ML 领域看到的碎片化问题。

作为一个开源项目，OpenXLA 遵循以下原则：

- 平等地位：个人无论从属关系如何，都平等地做出贡献。技术领导者是那些贡献最多时间和精力的人。
- 尊重文化：所有成员都应维护项目价值观和行为准则，无论他们在社区中的职位如何。
- 可扩展、高效的治理：小团队做出基于共识的决策，具有清晰但很少使用的升级路径。
- 透明度：所有决定和理由都应该对公众清晰可见。

**OpenXLA 生态系统：性能、规模和可移植能力**

OpenXLA 通过模块化工具链消除了机器学习开发人员的障碍，它通过通用编译器接口得到所有领先框架的支持，利用可移植的标准化模型表示，并提供具有强大的目标向和特定硬件优化的特定领域编译器。该工具链包括 XLA、StableHLO 和 IREE，所有这些工具都利用 MLIR：一种编译器基础架构，使机器学习模型能够在硬件上一致地表示、优化和执行。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9XnWoRbEQaayhrJicumwd46dudWbiaHqWkxKdVHzQ6y7icUa1KD3OicBevAYXSnsQibXia4M9gtztGWCiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**OpenXLA 主要亮点**

**机器学习用例的范围**

OpenXLA 当前的使用涵盖了 ML 用例的范围，包括在阿里云上对 DeepMind 的 AlphaFold、GPT2 和 Swin Transformer 等模型进行全面训练，以及在 Amazon.com 上进行多模态 LLM 训练。Waymo 等客户利用了 OpenXLA 进行车载实时推理。此外，OpenXLA 还用于优化配备 AMD RDNA™ 3 的本地机器上的 Stable Diffusion 服务。

**最佳性能，开箱即用**

OpenXLA 使开发人员无需编写特定于设备的代码，即可轻松加快模型性能。它具有整体模型优化功能，包括简化代数表达式、优化内存数据布局以及改进调度以减少峰值内存使用和通信开销。高级算子融合和内核生成有助于提高设备利用率并降低内存带宽要求。

**轻松扩展工作负载**

开发高效的并行化算法非常耗时并且需要专业知识。借助 GSPMD 等功能，开发人员只需注释关键张量的一个子集，然后编译器就可以使用这些子集自动生成并行计算。这消除了跨多个硬件主机和加速器对模型进行分区和高效并行化所需的大量工作。

**便携性和可选性**

OpenXLA 为多种硬件设备提供开箱即用的支持，包括 AMD 和 NVIDIA GPU、x86 CPU 和 Arm 架构以及 ML 加速器，如 Google TPU、AWS Trainium 和 Inferentia、Graphcore IPU、Cerebras Wafer-Scale Engine 等等。OpenXLA 还通过 StableHLO 支持 TensorFlow、PyTorch 和 JAX，StableHLO 是一个用作 OpenXLA 输入格式的可移植层。

**灵活性**

OpenXLA 为用户提供了手动调整模型热点的灵活性。自定义调用等扩展机制使用户能够用 CUDA、HIP、SYCL、Triton 和其他内核语言编写深度学习原语，从而能够充分利用硬件特性。

**StableHLO**

StableHLO 是 ML 框架和 ML 编译器之间的一个可移植层，是一个支持动态、量化和稀疏性的高级运算（HLO）的运算集。此外，它可以被序列化为 MLIR 字节码以提供兼容性保证。所有主要的 ML 框架（JAX、PyTorch、TensorFlow）都可以产生 StableHLO。2023 年，谷歌计划与 PyTorch 团队紧密合作，实现与 PyTorch 2.0 版本的整合。

**参考文献**：

[1] https://opensource.googleblog.com/2023/03/openxla-is-ready-to-accelerate-and-simplify-ml-development.html?m=1

[2] https://venturebeat.com/ai/google-reveals-whats-next-for-cloud-ai/

