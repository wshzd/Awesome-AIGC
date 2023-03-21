# GPT4_Technical_Detail

**GPT-4：我 SAT 考 710，也能当律师**

GPT-4 是一个大型多模态模型，能接受图像和文本输入，再输出正确的文本回复。实验表明，GPT-4 在各种专业测试和学术基准上的表现与人类水平相当。例如，它通过了模拟律师考试，且分数在应试者的前 10% 左右；相比之下，GPT-3.5 的得分在倒数 10% 左右。

OpenAI 花了 6 个月的时间使用对抗性测试程序和 ChatGPT 的经验教训对 GPT-4 进行迭代调整 ，从而在真实性、可控性等方面取得了有史以来最好的结果。

在过去的两年里，OpenAI 重建了整个深度学习堆栈，并与 Azure 一起为其工作负载从头开始设计了一台超级计算机。一年前，OpenAI 在训练 GPT-3.5 时第一次尝试运行了该超算系统，之后他们又陆续发现并修复了一些错误，改进了其理论基础。这些改进的结果是 GPT-4 的训练运行获得了前所未有的稳定，以至于 OpenAI 能够提前准确预测 GPT-4 的训练性能，它也是第一个实现这一点的大模型。OpenAI 表示他们将继续专注于可靠的扩展，进一步完善方法，以帮助其实现更强大的提前预测性能和规划未来的能力，这对安全至关重要。

OpenAI 正在通过 ChatGPT 和 API（有候补名单）发布 GPT-4 的文本输入功能。图像输入功能方面，为了获得更广泛的可用性，OpenAI 正在与其他公司展开合作。

OpenAI 今天还开源了 OpenAI Evals，这是其用于自动评估 AI 模型性能的框架。OpenAI 表示此举是为了让所有人都可以指出其模型中的缺点，以帮助 OpenAI 进一步改进模型。

有趣的是，GPT-3.5 和 GPT-4 之间的区别很微妙。当任务的复杂性达到足够的阈值时，差异就会出现 ——GPT-4 比 GPT-3.5 更可靠、更有创意，并且能够处理更细微的指令。为了了解这两个模型之间的差异，OpenAI 在各种基准和一些为人类设计的模拟考试上进行了实验。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQsucdPDloXgcqQs6Y45Nadjb3HCGv71N48zTNsaID4SFrCJytia5iabXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQCiaBcN0fiaiagE9z3H5ictraHq3xHAYYF4CLf4culSEibNuw0I5bQ1ObHhQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

OpenAI 还在为机器学习模型设计的传统基准上评估了 GPT-4。GPT-4 大大优于现有的大型语言模型，以及大多数 SOTA 模型：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQDEpdaK8HPH1ia5YIBgiacREtESJSTDCd1rZqC1zue8o7Cel4pn8UjRtQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

许多现有的机器学习基准测试都是用英语编写的。为了初步了解 GPT-4 在其他语言上的能力，研究团队使用 Azure Translate 将 MMLU 基准 —— 一套涵盖 57 个主题的 14000 个多项选择题 —— 翻译成多种语言。在测试的 26 种语言的 24 种中，GPT-4 优于 GPT-3.5 和其他大语言模型（Chinchilla、PaLM）的英语语言性能：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ6mIsXRQE7vxtswSa4U4z1odwUU5gvns3htA6AJffarnej7sP3keaVQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就像许多使用 ChatGPT 的公司一样，OpenAI 表示他们内部也在使用 GPT-4，因此 OpenAI 也在关注大型语言模型在内容生成、销售和编程等方面的应用效果。OpenAI 还使用 GPT-4 辅助人们评估 AI 输出，这也是 OpenAI 对其策略的第二阶段。OpenAI 既是 GPT-4 的开发者，也是使用者。

**GPT-4：我能玩梗图**

GPT-4 可以接受文本和图像形式的 prompt，新能力与纯文本设置并行，允许用户指定任何视觉或语言任务。

具体来说，它在人类给定由散布的文本和图像组成的输入的情况下生成相应的文本输出（自然语言、代码等）。在一系列领域 —— 包括带有文本和照片的文档、图表或屏幕截图上 ——GPT-4 展示了与纯文本输入类似的功能。此外，它还可以通过为纯文本语言模型开发的测试时间技术得到增强，包括少样本和思维链 prompt。

比如给 GPT-4 一个长相奇怪的充电器的图片，问为什么这很可笑？

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQCkibRrYhibJgAdSwD38NaYMcX68tg1a9y0qWMpAIaOtQicJXSGC415y0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

GPT-4 回答道，VGA 线充 iPhone。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ19Ny87ztoOO1NNpDqLsq0UVMIiahtoc2XASib9DCs3DYypscfchgwV6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

格鲁吉亚和西亚的人均每日肉类消费，算平均数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQczM849iciazf9czvBFUib9BCbc9Ddo3DM8QaPSXbdia5Sz9WGDa2icstEhw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来，现在的 GPT 已经不会在计算上胡言乱语了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQbQKd3ViaI6xFX38M8EozD87icaMKbC2vh0fkSaCduKV27ggAsdNzvIKQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还是太简单，那直接让它做题，还是个物理题：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ6BcnMNPH9O6up54tl0DtibHyD91N9hnjLZdhib478pGoEwKylictSGl3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

GPT-4 看懂了法语题目，并完整解答：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQAyicQwxa1BYx8zp7rzVIibIxKG4KCiclT5QAUCu2LSOVjGRBb2yCGCh0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

GPT-4 可以理解一张照片里「有什么不对劲的地方」：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQy93kxCXogiaUnCgaEXlfkMPFAnK0hKSQ3lHgeskylU5xa7BLTFCOxuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

GPT-4 还可以量子速读看论文，如果你给它 InstructGPT 的论文，让它总结摘要，就会变成这样：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQJl0horZtokSsiasicAyzGgboPibQKicmxmOk8MYz6B1rMearAQGSNcbKSw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQiap7DdRTbU3xicUvbKwU8QXFxRvOVr6WjibsfaxAHXxjo8jiaOELs7FEOA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果你对论文里的某一个图感兴趣呢？GPT-4 也可以解释一下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ6EX9J8rYgMWhKhfdPlctn09ibMLzrN5EIT9d0PMGlKGUksCM7tfyOJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

接着来，问 GPT-4 梗图是什么意思：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQvibEdf03YHLPZicP1vvaMCibNb1Wl12U26qPQfhBGhkd1zYMicyHWUMUdQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

它给出了详细的回答：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ94icOicLKicic3sicRZS3IEK5iaHHQXhyc8TOe6XOQ2tjXcWPm0a4Prib5tHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

那么漫画呢？

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQGSztlCl4jicn4uBU5b8x9hWI15BQgYPKC7ceJBPYoGaBkGYiagCwaib4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

让 GPT-4 解释为什么要给神经网络加层数，似乎有一点加倍的幽默感。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQSxiaVsiasxKWtV1Umc9FNwnVUXfB1ugRRJibpkFwvqSMiajichL5XccAMqA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不过 OpenAI 在这里说了，图像输入是研究预览，仍不公开。

研究人员用学术的 Benchmark 视角来解读 GPT-4 的看图能力，然而这已经不够了，他们还能不断发现该模型可以令人兴奋地处理新任务 —— 现在的矛盾是 AI 的能力和人类想象力之间的矛盾。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ6ZjyS30ZUoX1B13dCVkrR9SqPtglp6X1LFgrwTQYibtnlib9sqzgeEow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看到这里，应该有研究人员感叹：CV 不存在了。

**可控性**

与具有固定冗长、平静语气和风格的经典 ChatGPT 个性不同，开发人员（以及 ChatGPT 用户）现在可以通过在「系统」消息中描述这些方向来规定他们的 AI 的风格和任务。

系统消息允许 API 用户在一定范围内定制化实现不同的用户体验。OpenAI 知道你们在让 ChatGPT 玩 Cosplay，也鼓励你们这样做。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQlucgCzG1AiboIDVa9gzIUqcYD0OAuhLoyjpPibGHYNiaQEPwzCrmjlz1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**局限性**

尽管功能已经非常强大，但 GPT-4 仍与早期的 GPT 模型具有相似的局限性，其中最重要的一点是它仍然不完全可靠。OpenAI 表示，GPT-4 仍然会产生幻觉、生成错误答案，并出现推理错误。

目前，使用语言模型应谨慎审查输出内容，必要时使用与特定用例的需求相匹配的确切协议（例如人工审查、附加上下文或完全避免使用） 。

总的来说，GPT-4 相对于以前的模型（经过多次迭代和改进）已经显著减轻了幻觉问题。在 OpenAI 的内部对抗性真实性评估中，GPT-4 的得分比最新的 GPT-3.5 模型高 40%：

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ6VqyoPx0qU39pGfbf63M5cq4xMqdDg59rX2qicBuIbyoewWaZ1YAcHw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

GPT-4 在 TruthfulQA 等外部基准测试方面也取得了进展，OpenAI 测试了模型将事实与错误陈述的对抗性选择区分开的能力，结果如下图所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQXf0LxdG4w2TRRdOt5j8LxWEtQukTsgmM43UBy6RHe5o48EbFFYEq3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

实验结果表明，GPT-4 基本模型在此任务上仅比 GPT-3.5 略好；然而，在经过 RLHF 后训练之后，二者的差距就很大了。以下是 GPT-4 的测试示例 —— 并不是所有时候它都能做出正确的选择。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQdY6Nzac60rg7Ce2LaTxhsVYBcm3nvFib7jAy5XribPIrPbHmhBC20kYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

该模型在其输出中可能会有各种偏见，OpenAI 在这些方面已经取得了进展，目标是使建立的人工智能系统具有合理的默认行为，以反映广泛的用户价值观。

GPT-4 通常缺乏对其绝大部分数据截止后（2021 年 9 月）发生的事件的了解，也不会从其经验中学习。它有时会犯一些简单的推理错误，这似乎与这么多领域的能力不相符，或者过于轻信用户的明显虚假陈述。有时它也会像人类一样在困难的问题上失败，比如在它生成的代码中引入安全漏洞。

GPT-4 预测时也可能出错但很自信，意识到可能出错时也不会 double-check。有趣的是，基础预训练模型经过高度校准（其对答案的预测置信度通常与正确概率相匹配）。然而，通过 OpenAI 目前的后训练（post-training）过程，校准减少了。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

**风险及缓解措施**

OpenAI 表示，研究团队一直在对 GPT-4 进行迭代，使其从训练开始就更加安全和一致，所做的努力包括预训练数据的选择和过滤、评估和专家参与、模型安全改进以及监测和执行。

GPT-4 有着与以前的模型类似的风险，如产生有害的建议、错误的代码或不准确的信息。同时，GPT-4 的额外能力导致了新的风险面。为了了解这些风险的程度，团队聘请了 50 多位来自人工智能对齐风险、网络安全、生物风险、信任和安全以及国际安全等领域的专家，对该模型在高风险领域的行为进行对抗性测试。这些领域需要专业知识来评估，来自这些专家的反馈和数据为缓解措施和模型的改进提供了依据。

**预防风险**

按照 demo 视频里 OpenAI 工程师们的说法，GPT-4 的训练在去年 8 月完成，剩下的时间都在进行微调提升，以及最重要的去除危险内容生成的工作。

GPT-4 在 RLHF 训练中加入了一个额外的安全奖励信号，通过训练模型拒绝对此类内容的请求来减少有害的输出。奖励是由 GPT-4 的零样本分类器提供的，它判断安全边界和安全相关 prompt 的完成方式。为了防止模型拒绝有效的请求，团队从各种来源（例如，标注的生产数据、人类的红队、模型生成的 prompt）收集多样化的数据集，在允许和不允许的类别上应用安全奖励信号（有正值或负值）。

这些措施大大在许多方面改善了 GPT-4 的安全性能。与 GPT-3.5 相比，模型对不允许内容的请求的响应倾向降低了 82%，而 GPT-4 对敏感请求（如医疗建议和自我伤害）的响应符合政策的频率提高了 29%。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQ6ibUcRsBcOqp0jmQLkTq40jsp9bwlYib8VNm5mGpdg2lmbvzu9bArELA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**训练过程**

与之前的 GPT 模型一样，GPT-4 基础模型经过训练可以预测文档中的下一个单词。OpenAI 使用公开可用的数据（例如互联网数据）以及已获得许可的数据进行训练。训练数据是一个网络规模的数据语料库，包括数学问题的正确和错误解决方案、弱推理和强推理、自相矛盾和一致的陈述，以及各种各样的意识形态和想法。

因此，当提出问题时，基础模型的回应可能与用户的意图相去甚远。为了使其与用户意图保持一致，OpenAI 依然使用强化学习人类反馈 (RLHF) 来微调模型的行为。请注意，该模型的能力似乎主要来自预训练过程 ——RLHF 不会提高考试成绩（甚至可能会降低它）。但是模型的控制来自后训练过程 —— 基础模型甚至需要及时的工程设计来回答问题。

GPT-4 的一大重点是建立了一个可预测扩展的深度学习栈。主要原因是，对于像 GPT-4 这样的大型训练，进行广泛的特定模型调整是不可行的。团队开发了基础设施和优化，在多种规模下都有可预测的行为。为了验证这种可扩展性，他们提前准确地预测了 GPT-4 在内部代码库（不属于训练集）上的最终损失，方法是通过使用相同的方法训练的模型进行推断，但使用的计算量为 1/10000。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

现在，OpenAI 可以准确地预测在训练过程中优化的指标（损失）。例如从计算量为 1/1000 的模型中推断并成功地预测了 HumanEval 数据集的一个子集的通过率：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

有些能力仍然难以预测。例如，Inverse Scaling 竞赛旨在找到一个随着模型计算量的增加而变得更糟的指标，而 hindsight neglect 任务是获胜者之一。GPT-4 扭转了这一趋势。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQcrqInY8ibyh1BBBBwzNwU6kVVRpjO5hB7O57ho8o0a6HEPCgVbCzibVQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

能够准确预测未来的机器学习能力对于技术安全来说至关重要，但它并没有得到足够的重视，OpenAI 表示正在投入更多精力开发相关方法，并呼吁业界共同努力。

OpenAI 表示正在开源 OpenAI Evals 软件框架，它被用于创建和运行基准测试以评估 GPT-4 等模型，同时可以逐样本地检查模型性能。

**ChatGPT 直接升级至 GPT-4 版**

GPT-4 发布后，OpenAI 直接升级了 ChatGPT。ChatGPT Plus 订阅者可以在 chat.openai.com 上获得具有使用上限的 GPT-4 访问权限。

要访问 GPT-4 API（它使用与 gpt-3.5-turbo 相同的 ChatCompletions API），用户可以注册等待。OpenAI 会邀请部分开发者体验。

获得访问权限后，用户目前可以向 GPT-4 模型发出纯文本请求（图像输入仍处于有限的 alpha 阶段）。至于价格方面，定价为每 1k 个 prompt token 0.03 美元，每 1k 个 completion token 0.06 美元。默认速率限制为每分钟 40k 个 token 和每分钟 200 个请求。

GPT-4 的上下文长度为 8,192 个 token。OpenAI 还提供了 32,768 个 token 上下文（约 50 页文本）版本的有限访问，该版本也将随着时间自动更新（当前版本 gpt-4-32k-0314，也支持到 6 月 14 日)。定价为每 1K prompt token 0.06 美元和每 1k completion token 0.12 美元。

以上，就是今天 OpenAI 关于 GPT-4 的所有内容了。令人不满的一点是，OpenAI 公开的技术报告中，不包含任何关于模型架构、硬件、算力等方面的更多信息，可以说是很不 Open 了。

不管怎样，迫不及待的用户大概已经开始测试体验了吧。

![图片](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW9IKEQMJCN2Otv1uqdzMUYQWqdAAK42ww9svEhm3LPOK6ib6JumQxXjuPicsSOGv1l6YHIS7icnjTQFA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

最后，也想问一下读者，看完 GPT-4 的发布，你有何感想。

*参考内容：**https://openai.com/product/gpt-4*









