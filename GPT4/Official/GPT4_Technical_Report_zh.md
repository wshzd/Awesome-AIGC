# GPT4_Technical_Report_zh

我们创建了 GPT-4，这是 OpenAI 努力扩展深度学习的最新里程碑。GPT-4 是一个大型多模态模型（接受图像和文本输入，发出文本输出），虽然在许多现实世界场景中的能力不如人类，但在各种专业和学术基准上表现出人类水平的表现。例如，它通过模拟律师考试，分数在应试者的前 10% 左右；相比之下，GPT-3.5 的得分在倒数 10% 左右。我们花了 6 个月的时间使用我们的对抗性测试程序和 ChatGPT 的经验教训迭代[对齐](https://openai.com/research/instruction-following) GPT-4，从而在真实性、可操纵性和拒绝超出安全方面取得了有史以来最好的结果（尽管远非完美）。

在过去的两年里，我们重建了整个深度学习堆栈，并与 Azure 一起从头开始为我们的工作负载共同设计了一台超级计算机。一年前，我们训练 GPT-3.5 作为系统的第一次“试运行”。我们发现并修复了一些错误并改进了我们的理论基础。结果，我们的 GPT-4 训练运行（至少对我们而言！）前所未有地稳定，成为我们能够提前准确预测其训练性能的第一个大型模型。随着我们继续专注于可靠的扩展，我们的目标是完善我们的方法，以帮助我们越来越多地提前预测和准备未来的能力——我们认为这对安全至关重要。

我们正在通过 ChatGPT 和 API（有[候补名单](https://openai.com/waitlist/gpt-4-api)）发布 GPT-4 的文本输入功能。为了准备图像输入功能以获得更广泛的可用性，我们正在与[一个合作伙伴](https://www.bemyeyes.com/)密切合作。我们还开源了[OpenAI Evals](https://github.com/openai/evals)，这是我们用于自动评估 AI 模型性能的框架，允许任何人报告我们模型中的缺点，以帮助指导进一步改进。

## **能力**

在随意的谈话中，GPT-3.5 和 GPT-4 之间的区别可能很微妙。当任务的复杂性达到足够的阈值时，差异就会出现——GPT-4 比 GPT-3.5 更可靠、更有创意，并且能够处理更细微的指令。为了了解这两种模型之间的区别，我们在各种基准测试中进行了测试，包括最初为人类设计的模拟考试。我们通过使用最新的公开测试（在奥林匹克竞赛和 AP 自由回答问题的情况下）或购买 2022-2023 年版本的练习考试来继续。我们没有针对这些考试进行专门训练。模型在训练期间看到了考试中的一小部分问题，但我们认为结果具有代表性——有关详细信息，请参阅我们的[技术报告](https://cdn.openai.com/papers/gpt-4.pdf)。

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAqzcLbhNFCDKAewhX4bnoKSqLf78ZEPGgzlHGwIq6tswoW0ZibZic2FxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAHlDIXcwVYxPicTjkTLMJPzTsd5p7eibmdnYDyiaSysgrD5UpQk9HsJd0g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAiclwRk5oaFuLcziao7VcjwWrBGnO7Ej9PcBmyngDkl9X9iahmQGx79xww/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAYpeOkIwx7kQNUEl1kBE10qxwrfQibxRsbSkiahEusfsnx16A1MfRL6WA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

我们还在为机器学习模型设计的传统基准上评估了 GPT-4。GPT-4 大大优于现有的大型语言模型，以及大多数最先进的 (SOTA) 模型，其中可能包括特定于基准的制作或额外的训练协议：

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicALDjjCPsWUyh9pia9fhMGkONQzCrunyQAZyq6GkFOffvlBd1kHmpDczg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

许多现有的 ML 基准测试都是用英语编写的。为了初步了解其他语言的能力，我们使用 Azure Translate（参见[附录](https://openai.com/research/gpt-4#appendix)）将 MMLU 基准——一套涵盖 57 个主题的 14,000 个多项选择题——翻译成多种语言。在测试的 26 种语言中的 24 种中，GPT-4 优于 GPT-3.5 和其他 LLM（Chinchilla、PaLM）的英语语言性能，包括拉脱维亚语、威尔士语和斯瓦希里语等低资源语言：

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAybFMEVUlVViaVdQveicJuO4AMjvEbWdk8TdNHMCk208ftdw3qEJQjsYA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

我们也在内部使用 GPT-4，对支持、销售、内容审核和编程等功能产生了巨大影响。我们还使用它来帮助人类评估 AI 输出，开始我们[对齐策略](https://openai.com/blog/our-approach-to-alignment-research)的第二阶段。

### **视觉输入**

GPT-4 可以接受文本和图像提示，这与纯文本设置并行，允许用户指定任何视觉或语言任务。具体来说，它在给定由散布的文本和图像组成的输入的情况下生成文本输出（自然语言、代码等）。在一系列领域——包括带有文本和照片、图表或屏幕截图的文档——GPT-4 展示了与纯文本输入类似的功能。此外，它还可以通过为纯文本语言模型开发的测试时间技术得到增强，包括少量镜头和[思维链](https://arxiv.org/abs/2201.11903)提示。图像输入仍然是研究图像预览，不公开。

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAC5Kt23tdZ36AQawJOoWewzderJm65EX5HmLX92A5xsLggGdrgolnNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAMw6Wkhn6JQ9iaSZGlWXicz6rrMthTRLvOep36aickheTeX53S6Q4TLYPQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicANjE8H1InON7KEc6e5Ra4Hn9ZMwGRYqmxkVsjFScoZujx6lkDyQ8ncg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAHJuXOCoXzD3SOHAnRogqDmQrnuxem75el9lIs1RxibDiaphNfZxeZF7w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAicptCJe7Z6ROicgkpHZVe2L8bjNaEaGRrnJetpJDWvdRiaWv8SHDjhS0g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicA0GubFlCT7en870NPmvDKV8jYLNPKoMhnibCAPhvH8N9fWX0I2okdbfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicA09lGN2DFft2n9ggQkiaU3iaFBQFormkNs91g5eQCPdaxudQJLt9jsMLw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

我们通过在一套狭义的标准学术视觉基准上对其进行评估来预览 GPT-4 的性能。然而，这些数字并不能完全代表其能力范围，因为我们不断发现该模型能够处理的新的和令人兴奋的任务。我们计划很快发布进一步的分析和评估数据，并彻底调查测试时间技术的影响。

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicANYhA63wrZ5icDy6vsTCbMWxWjcg4YEfhd7thiclexXXmRCQViaN6SyrQA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### **操纵性**

我们一直致力于我们关于[定义 AI 行为](https://openai.com/blog/how-should-ai-systems-behave)的帖子中概述的计划的各个方面，包括可操纵性。与具有固定冗长、语气和风格的经典 ChatGPT 个性不同，开发人员（以及很快的 ChatGPT 用户）现在可以通过在“系统”消息中描述这些方向来规定他们的 AI 的风格和任务。系统消息允许 API 用户在[一定范围](https://platform.openai.com/docs/usage-policies)内显着定制他们的用户体验。我们将在这里不断改进（特别是知道系统消息是“越狱”当前模型的最简单方法，即对边界的遵守并不完美），但我们鼓励您尝试一下并让我们知道您认为。

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAVbZu0DovdNxCBdDgS0FqgvcT1XyffAiazhXjDToRiauZYroTuiblEuSEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAXXoHwNUK5B9I1EwdTFlubhKOE12FbztpmqBZjtBeuiby8fq7ZiciaQXIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAJrdrzcePzFicsSiaDsBCSZ3icRUncHQ5JKaicBOVtyEPgnSpNJ0wfKeZyA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAXoIpUWmvc6ltibYQXt1XYsIfRO8D6HQZZvibc7Nl1NhgNNTibdlM5jp5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAZcicrhnKyibhoPSDcdh2KoK5gno4wDUqsYpbpfY1BaiamNwjIbTiaGgosw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAksoy2BIGSOCOAHxPURXM4unUurqNJ9PyEhIRibicZ0YBFNFTJtxTZMsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## **限制**

尽管功能强大，但 GPT-4 与早期的 GPT 模型具有相似的局限性。最重要的是，它仍然不完全可靠（它“幻觉”事实并出现推理错误）。在使用语言模型输出时应格外小心，特别是在高风险上下文中，使用与特定用例的需求相匹配的确切协议（例如人工审查、附加上下文的基础或完全避免高风险使用）。

虽然仍然是一个真正的问题，但 GPT-4 相对于以前的模型（它们本身在每次迭代中都在改进）显着减少了幻觉。在我们的内部对抗性真实性评估中，GPT-4 的得分比我们最新的 GPT-3.5 高 40%：

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAHtakK4YjgicYw9w7ArFEfCtR1ONrL05ENHZqpgNTRM5FVDhDzKasAlg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

我们在 TruthfulQA 等外部基准测试方面取得了进展，它测试了模型将事实与对抗性选择的一组错误陈述分开的能力。这些问题与事实不正确的答案配对，这些答案在统计上很有吸引力。

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicA4HPYiaibMnWfBVtD6rkkcodpjjibBkpxic38yc7QZQOfqaxdd7abcfzNIw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

GPT-4 基本模型在此任务上仅比 GPT-3.5 略好；然而，在[RLHF](https://openai.com/research/learning-from-human-preferences)后训练（使用与[GPT-3.5](https://openai.com/blog/chatgpt)相同的过程）之后，存在很大差距。检查下面的一些例子，GPT-4 拒绝选择俗语（你不能教老狗新把戏），但它仍然会遗漏细微的细节（猫王不是演员的儿子）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAfIyNbHjb7aP9VWQeyYBHiamtdUQm5OiaYgnNDsfhNEJiaM0D9NWWjFpvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

该模型的输出可能存在各种偏差——我们在这些方面取得了进展，但还有更多工作要做。根据我们[最近的博客文章](https://openai.com/blog/how-should-ai-systems-behave)，我们的目标是让我们构建的 AI 系统具有合理的默认行为，以反映广泛的用户价值观，允许这些系统在广泛的范围内进行定制，并就这些范围应该是什么获得公众意见。GPT-4 普遍缺乏对绝大部分数据中断后（2021 年 9 月）发生的事件的了解，也没有从经验中吸取教训。它有时会犯一些简单的推理错误，这些错误似乎与跨多个领域的能力不相称，或者在接受用户明显的虚假陈述时过于轻信。有时它会像人类一样在难题上失败，例如在它生成的代码中引入安全漏洞。GPT-4 也可能自信地在其预测中犯错，在可能出错时不注意仔细检查工作。有趣的是，基础预训练模型经过高度校准（其对答案的预测置信度通常与正确概率相匹配）。然而，通过我们目前的训练后过程，校准减少了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicA2ictRvia3lXIBVO1w8WzcBDDLbl28JAzJ1w5aDCaGOMse86o4C7sQLXA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## **风险与缓解措施**

我们一直在对 GPT-4 进行迭代，以使其从训练开始就更安全、更一致，工作包括预训练数据的选择和过滤、评估和专家参与、模型安全改进以及监控和执行。

GPT-4 会带来与之前模型类似的风险，例如生成有害建议、错误代码或不准确信息。但是，GPT-4 的附加功能会带来新的风险面。为了了解这些风险的程度，我们聘请了 50 多位来自 AI 对齐风险、网络安全、生物风险、信任和安全以及国际安全等领域的专家来对模型进行对抗性测试。他们的发现特别使我们能够在需要专业知识进行评估的高风险领域测试模型行为。这些专家的反馈和数据用于我们对模型的缓解和改进；例如，我们收集了额外的数据来提高 GPT-4 拒绝有关如何合成危险化学品的请求的能力。

GPT-4 在 RLHF 训练期间加入了一个额外的安全奖励信号，通过训练模型拒绝对此类内容的请求来减少有害输出（如我们的[使用指南所定义](https://platform.openai.com/docs/usage-policies/disallowed-usage)）。奖励由 GPT-4 零样本分类器提供，该分类器根据安全相关提示判断安全边界和完成方式。为了防止模型拒绝有效请求，我们从各种来源（例如，标记的生产数据、人类红队、模型生成的提示）收集了多样化的数据集，并在两者上应用安全奖励信号（具有正值或负值）允许和不允许的类别。

与 GPT-3.5 相比，我们的缓解措施显着改善了 GPT-4 的许多安全特性。与 GPT-3.5 相比，我们已将模型响应不允许内容请求的倾向降低了 82%，并且 GPT-4 根据我们的政策响应敏感请求（例如，医疗建议和自我伤害）的频率提高了 29%

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicA77afWzOGiaoge3DcCkAFZtggDzaNSfYH6cW9GibkYEBnRyCBOKKuUROQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAQHIrgOxILEUoIJLJkzAAab8fJ9ObhF9IiaLBXxPdia8X2kPfE9iaVAOtA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

总的来说，我们的模型级干预增加了引发不良行为的难度，但这样做仍然是可能的。此外，仍然存在生成违反我们[使用指南](https://openai.com/policies/usage-policies)的内容的“越狱” 。随着人工智能系统“每个代币的风险”增加，在这些干预中实现极高的可靠性将变得至关重要；目前，重要的是用部署时安全技术（如监控滥用）来补充这些限制。

GPT-4 和后续模型有可能以有益和有害的方式对社会产生重大影响。我们正在与外部研究人员合作，以改进我们理解和评估潜在影响的方式，以及对未来系统中可能出现的危险功能进行评估。我们很快将分享更多关于 GPT-4 和其他人工智能系统的潜在社会和经济影响的想法。

## **训练过程**

与以前的 GPT 模型一样，GPT-4 基础模型经过训练可以预测文档中的下一个单词，并且使用公开可用的数据（例如互联网数据）以及我们已获得许可的数据进行训练。这些数据是网络规模的数据语料库，包括数学问题的正确和错误解决方案、弱推理和强推理、自相矛盾和一致的陈述，并代表各种各样的意识形态和想法。

因此，当出现问题提示时，基本模型可以以多种可能与用户意图相去甚远的方式做出响应。为了使其与护栏内的用户意图保持一致，我们使用[强化学习和人工反馈 ( RLHF )](https://openai.com/research/learning-from-human-preferences)来微调模型的行为。

请注意，该模型的能力似乎主要来自预训练过程——RLHF 不会提高考试成绩（如果不积极努力，它实际上会降低考试成绩）。但是模型的控制来自训练后过程——基础模型需要及时的工程设计甚至知道它应该回答问题。

### **可预测的扩展**

GPT-4 项目的一大重点是构建可预测扩展的深度学习堆栈。主要原因是，对于像 GPT-4 这样的非常大的训练运行，进行广泛的特定于模型的调整是不可行的。我们开发的基础设施和优化在多个尺度上具有非常可预测的行为。为了验证这种可扩展性，我们通过从使用相同方法训练但使用 10,000 倍更少计算的模型进行推断，准确预测了 GPT-4 在我们内部代码库（不是训练集的一部分）上的最终损失：

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAEpDVogOoPN0DwtqnPmiaZvUUSCdDkmH7vAfiaBibdicVibibpW8zKg1VOICA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在我们可以准确地预测我们在训练期间优化的指标（损失），我们开始开发方法来预测更多可解释的指标。例如，我们成功预测了[HumanEval](https://github.com/openai/human-eval)数据集子集的通过率，从计算量减少 1,000 倍的模型推断：

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAtqpxaibF8bqHbnLd9dAJWe2M4zyy3RCtaLicjllZ74iat4UyqqhPm4sfQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有些能力仍然难以预测。例如，Inverse Scaling Prize 是一项竞赛，目的是寻找一个随着模型计算量的增加而变得更糟的指标，而[hindsight neglect](https://www.alignmentforum.org/posts/iznohbCPFkeB9kAJL/inverse-scaling-prize-round-1-winners#_The_Floating_Droid___for_hindsight_neglect_10shot)是赢家之一。就像最近的[另一个结果](https://arxiv.org/abs/2211.02011)一样， GPT-4 扭转了趋势：

![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAkee1PMQddjCvPS3Nuyg2AtrIIL4GfRK8ichVF9HhzRxgHEh0DniaVkOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

我们认为，准确预测未来的机器学习能力是安全的重要组成部分，但相对于其潜在影响而言，它并没有得到足够的重视（尽管我们受到了多个机构的努力的鼓舞）。我们正在加大力度开发方法，为社会提供更好的未来系统预期指导，我们希望这成为该领域的共同目标。

## **OpenAI 评估**

我们正在开源[OpenAI Evals](https://github.com/openai/evals)，这是我们的软件框架，用于创建和运行基准测试以评估 GPT-4 等模型，同时逐个样本地检查它们的性能。我们使用 Evals 来指导我们模型的开发（识别缺点和防止回归），我们的用户可以应用它来跟踪模型版本（现在将定期发布）的性能和不断发展的产品集成。例如，Stripe 使用 Evals 来补充他们的人工评估，以衡量其基于 GPT 的文档工具的准确性。由于代码全部开源，Evals 支持编写新的类来实现[自定义评估逻辑](https://github.com/openai/evals/blob/main/docs/custom-eval.md)。然而，根据我们自己的经验，许多基准测试都遵循少数“模板”之一，因此我们还包括了内部最有用的模板（包括“模型分级评估”模板——我们发现 GPT- 4 令人惊讶地能够检查自己的工作）。通常，[构建新评估](https://github.com/openai/evals/blob/main/docs/build-eval.md)的最有效方法是实例化这些模板之一并提供数据。我们很高兴看到其他人可以使用这些模板和更普遍的 Evals 构建什么。我们希望 Evals 成为共享和众包基准测试的工具，代表最广泛的故障模式和困难任务。作为要遵循的示例，我们创建了一个[逻辑难题](https://github.com/openai/evals/blob/main/evals/registry/evals/logic.yaml)eval，其中包含十个 GPT-4 失败的提示。Evals 还与实施现有基准兼容；我们已经包含了几个实施学术基准的[笔记本](https://github.com/openai/evals/tree/main/examples)和一些集成[CoQA](https://github.com/openai/evals/blob/main/evals/registry/evals/coqa-ex.yaml) （的小子集）的变体作为示例。我们邀请所有人使用 Evals 来测试我们的模型并提交最有趣的示例。我们相信 Evals 将成为使用和构建我们模型的过程中不可或缺的一部分，我们欢迎直接贡献、问题和[反馈](https://github.com/openai/evals)。

## **ChatGPT Plus**

ChatGPT Plus 订阅者将在 chat.openai.com 上获得具有使用上限的 GPT-4 访问权限。我们将根据实践中的需求和系统性能调整确切的使用上限，但我们预计会受到严重的容量限制（尽管我们将在接下来的几个月内进行扩展和优化）。根据我们看到的流量模式，我们可能会为更高容量的 GPT-4 使用引入新的订阅级别；我们也希望在某个时候提供一些免费的 GPT-4 查询，这样那些没有订阅的人也可以尝试一下。

## **API**

要访问 GPT-4 API（它使用与 gpt-3.5-turbo 相同的[ChatCompletions API](https://platform.openai.com/docs/guides/chat/chat-vs-completions)），请[注册我们的候补名单](https://openai.com/waitlist/gpt-4)。我们今天将开始邀请一些开发人员，并逐步扩大规模以平衡容量与需求。如果您是研究 AI 的社会影响或 AI 对齐问题的研究员，您还可以通过我们的[Researcher Access Program](https://share.hsforms.com/1b-BEAq_qQpKcfFGKwwuhxA4sk30)申请补贴访问。

获得访问权限后，您可以向 gpt-4 模型发出纯文本请求（图像输入仍处于有限的 alpha 阶段），随着时间的推移，我们会在制作新版本时自动将其更新为我们推荐的稳定模型（您可以固定当前版本通过调用 gpt-4-0314，我们将支持到 6 月 14 日）。定价为每 1k 个提示令牌 0.03 美元和每 1k 个完成令牌 0.06 美元。默认速率限制为每分钟 40k 个令牌和每分钟 200 个请求。

gpt-4 的上下文长度为 8,192 个标记。我们还提供对我们的 32,768-上下文（约 50 页文本）版本 gpt-4-32k 的有限访问，该版本也将随着时间的推移自动更新（当前版本 gpt-4-32k-0314，也支持到 6 月 14 日). 定价为每 1K 提示令牌 0.06 美元和每 1k 完成令牌 0.12 美元。我们仍在提高长期上下文的模型质量，并希望得到有关它在您的用例中表现如何的反馈。我们正在根据容量以不同的速率处理对 8K 和 32K 引擎的请求，因此您可能会在不同时间获得对它们的访问权限。

## **结论**

我们期待 GPT-4 成为一个有价值的工具，通过为许多应用程序提供动力来改善人们的生活。还有很多工作要做，我们期待通过社区在该模型之上构建、探索和贡献的集体努力来改进该模型。

## **附录**

MMLU 问题示例，已翻译成其他语言。请注意，我们使用一致的选择标记 (A–D)：![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAg0kgxBicK9UnCpOI0JKYERicAbetYwpNTfhhZcrib9VOGGjb2SYLYl0aw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/N5aX12H1SicmSpspibqCHeAfG3Vmib8kpicAal69ID1hIg3icjGHCG4QlO5oCvGqZfibNH7kjHjSTgC5fAIrADMCbibpw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**GPT4相关资料**

**官网地址**：*https://openai.com/product/gpt-4*

**论文下载**：https://cdn.openai.com/papers/gpt-4.pdf

**直播地址**：https://www.youtube.com/watch?v=outcGtbnMuQ

**直播速记稿：**https://event-cdn.baai.ac.cn/file/file-browser/MhyB8XrtJbfpwiKYzGSCMJDS2kQ3mJ6y.pdf 

**贡献者**：https://openai.com/contributions/gpt-4

**开源Evals****框架**：https://github.com/openai/evals

**必应运行**：http://bing.com/new 

**更多地址：**

**View system card**：https://cdn.openai.com/papers/gpt-4-system-card.pdf

**Try on ChatGPT Plus**：https://chat.openai.com/chat

**Join API waitlist**：https://openai.com/waitlist/gpt-4-api

**Rewatch developer demo livestream**：https://youtube.com/live/outcGtbnMuQ?feature=share