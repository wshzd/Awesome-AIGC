# AIGC-Summary
## 介绍

自2022年11月份OpenAI公布ChatGPT以来，ChatGPT在五天之内注册用户数就突破了百万

![ChatGPT](images/chatgpt.png)

由此拉开了AIGC大模型的序幕，也有人称为是AI2.0时代，2023年3月14日又发布了GPT4，性能进一步得到提升，关于ChatGPT和GPT4为代码的文本生成以及Codex的代码生成等博客和论文层出不穷，这里对一些重点资料进行了整理归类，持续更新中......

## 中国版ChatGPT

无需注册即可体验ChatGPT效果的一些网站
* http://chat.h2ai.cn/home
* https://chat.forchange.cn/
* https://aigcfun.com/
* https://xc.com/
## Table of Contents

- [AGI](#agi)

  - [开源工具](#开源工具)

  - [相关博客及论文](#相关博客及论文)
- [AIGC相关会议](aigc相关会议)
- [Prompt工程](#prompt工程)
- [LLM体验效果](#llm体验效果)
- [Text](#Text)

  - [ChatGPT](#chatgpt)
    - [ChatGPT_Blogs](#chatgpt_blogs)
      - [ChatGPT_Application](#chatgpt_application)
      - [ChatGPT_Technology](#chatgpt_technology)
      - [ChatGPT_Other](#chatgpt_other)
    - [ChatGPT测试体验](#chatgpt测试体验)
    - [ChatGPT性能评估](#chatgpt性能评估)
    - [ChatGPT_Papers](#chatgpt_papers)
  - [GPT4](#gpt4)
    - [GPT4_Official_docs](#gpt4_official_docs)
    - [GPT4_Blogs](#gpt4_blogs)

    - [GPT4_Papers](#gpt4_papers)
  - [ChatGPT扩展模型](#chatgpt扩展模型)
  - [Bard](#bard)
  - [Claude](#claude)
  - [ChatGLM](#chatglm)
  - [ChatLLaMA](#chatllama)
  - [OpenChatKit](#openchatkit)
  - [LLM文本检测](#llm文本检测)
- [Picture&Video](#picture&video)


- [Code](#code)


- [Music](#music)


## AGI

- ### 开源工具

  - [Google发布统计深度学习框架平台：OpenXLA](https://github.com/wshzd/ChatGPT-Summary/blob/main/AGI/Google_OpenXLA.md)

- ### 相关博客及论文

- 【斯坦福大学研究大语言模型反映了谁的观点？】[[paper](https://arxiv.org/pdf/2303.17548.pdf)]，[[code](https://github.com/tatsu-lab/opinions_qa )]

- 【NAACL & ACL：大模型的两种知识继承方案】[[方案一](https://aclanthology.org/2022.naacl-main.288/)]，[[方案二](https://aclanthology.org/2022.acl-long.151/)]

- 【斯坦福大学 | 大模型及其公平使用】[[paper](https://arxiv.org/pdf/2303.15715.pdf )]

- 【斯坦福构建大模型生态系统图，用于跟踪大模型的足迹】[[blog](https://crfm.stanford.edu/ecosystem-graphs/index.html?mode=home)]

- 【大模型微调指南：当GPU资源不足时的有效解决方案】[[paper](https://arxiv.org/pdf/2303.15647.pdf )]

- 【纽约大学&Anthropic等提出ILF（从语言反馈中模仿学习）：利用语言反馈大规模训练语言模型】[[paper](https://arxiv.org/pdf/2303.16755.pdf )]

- 【微软亚研院首席研究员：一种新的大语言模型NLG评估框架】[[paper](https://arxiv.org/abs/2303.16634 )]

- 【**TaskMatrix.AI: Completing Tasks by Connecting Foundation Models with Millions of APIs** 】[[paper](https://arxiv.org/pdf/2303.16434.pdf )]

- 【**AnnoLLM: Making Large Language Models to Be Better Crowdsourced Annotators** 】[[paper](https://arxiv.org/pdf/2303.16854.pdf )]

- 【LLM，压缩即泛化，泛化即智能】[[blog](https://mp.weixin.qq.com/s/tSj9npIPg8IlYr2jbtg-Og)]

- 【智慧信息的压缩：模型智能的涌现之道】[[blog](https://mp.weixin.qq.com/s/hQmvltuMlClBonM6UJmtLg)]

- 【万字长文：想训大模型？这里有一份避坑指南】[[blog](https://mp.weixin.qq.com/s/yX5B1ZzV7vewQs1-ezHIQg)]

- 【拨动大模型的琴弦｜Delta Tuning 成果登上 Nature子刊封面！】[[blog](https://mp.weixin.qq.com/s/m3fNselWKQ2m5XnBe79fQQ)]

- 【Huawei | PanGu-Σ: 稀疏异构计算万亿参数语言模型研究参数语言模型】[[paper](https://arxiv.org/abs/2303.10845 )]

- 【大型人工智能模型中出现的不可预测的能力】[[blog]([https://www.quantamagazine.org/the-unpredictable-abilities-emerging-from-large-ai-models-20230316/ ](https://www.quantamagazine.org/the-unpredictable-abilities-emerging-from-large-ai-models-20230316) )]

- 【OpenAI | GPT就是GPT：大模型对劳动力市场影响潜力的早期研究】[[paper](https://arxiv.org/pdf/2303.10130.pdf )]

- 【ABC News 专访OpenAI首席执行官萨姆·奥尔特曼：AI风险和重塑社会的问题】[[blog](https://abcnews.go.com/Technology/openai-ceo-sam-altman-ai-reshape-society-acknowledges/story?id=97897122)]

- 【为什么现在的大语言模型（LLM）都是Decoder-only的架构？】[[blog](https://mp.weixin.qq.com/s/ZsHX-M9pisUvG9vqfzdzTQ)]

- 【微软 & Meta | ART：大型语言模型的自动多步骤推理和工具使用】[[paper](https://arxiv.org/pdf/2303.09014.pdf)]

- 【LeCun点赞：人工智能系统最终是否需要以现实为基础，而不仅仅是从语言中学习？】[[blog](https://spectrum.ieee.org/ai-hallucination )]

- 【斯坦福报告：基础模型的机遇与风险】[[blog](https://mp.weixin.qq.com/s/iEwvkqMT7KEqmnHk8NVz6w)]

- 【剑桥大学｜奖励聊天机器人在现实世界中与数以百万计的用户进行互动】[[paper](https://arxiv.org/pdf/2303.06135.pdf )]

- 【谷歌｜面向决策的基础模型: 问题、方法与机会】[[paper]( <https://arxiv.org/abs/2303.04129 )]

- 【大型语言模型的涌现能力】[[blog](https://www.assemblyai.com/blog/emergent-abilities-of-large-language-models/)]

- 【谷歌｜较大语言模型上下文学习的方式有所不同】[[paper]([https://arxiv.org/abs/2303.03846](https://arxiv.org/abs/2303.03846%C2%A0%C2%A0) )]

- 【谷歌发布5620亿参数多模态模型PaLM-E，机器人操控再上台阶】[[paper](https://arxiv.org/abs/2303.03378 )]，[[blog](https://palm-e.github.io/ )]，[[twitter](https://twitter.com/DannyDriess/status/1632904675124035585 )]，[[video](https://mp.weixin.qq.com/s/yZt3sEQPzVjnIvqXsNOnPA )]

- 【谷歌｜通用语音识别大模型已经支持100+语言】[[blog](https://mp.weixin.qq.com/s/fHr2vL-w4JtYt5utcZrbsw)]

- 【LeCun：ChatGPT无法实现通用人工智能，但ALM技术路线也许可以】[[blog](https://mp.weixin.qq.com/s/MEdl3zmiYJU1iFsTXmibng)]


- ### [OpenAI团队介绍](https://github.com/wshzd/ChatGPT-Summary/blob/main/AGI/OpenAI_Team.md)


- ### [OpenAI的AGI路线图](https://github.com/wshzd/ChatGPT-Summary/blob/main/AGI/OpenAI发布AGI路线图.md)

## AIGC相关会议

### 智源社区

【AugGPT：利用ChatGPT进行文本数据增强 】[[link](https://event.baai.ac.cn/activities/664 )]

【ChatGPT的鲁棒性探究——对抗性和分布外泛化的视角 】[[link](https://event.baai.ac.cn/activities/657 )]

【传统检索模型和大语言模型在信息搜索中的应用和对比 】[[link](https://event.baai.ac.cn/activities/656 )]

### DataFun



### 智东西



## Prompt工程

- 【OpenAI 应用人工智能研究负责人Lilian Weng新博文：关于提示工程的介绍】[[blog](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/)]
- 【Prompt Engineering全面自动化】[[blog](https://mp.weixin.qq.com/s/aj8Ls463jpF92ssn6Acwzg)]

## LLM体验效果

- 【人工智能聊天机器人比较：Bard vs. Bing vs. ChatGPT】[[blog](https://www.theverge.com/2023/3/24/23653377/ai-chatbots-comparison-bard-bing-chatgpt-gpt-4)]

- 【谷歌Bard_VS_百度文心一言】[[blog](https://mp.weixin.qq.com/s?__biz=Mzg3NDIyMzI0Mw==&mid=2247486260&idx=1&sn=a41224fee7ed4cb4a48eb40a420d7479&chksm=ced548d0f9a2c1c6f4930f30447468f9f01bb2af6031368e302b13a6354fc4bca6636e3b297e&token=666852558&lang=zh_CN#rd)]

- 【文心一言 VS ChatGLM-6B对比】[[blog](https://mp.weixin.qq.com/s?__biz=Mzg3NDIyMzI0Mw==&mid=2247486081&idx=2&sn=fd87305419158d66dd4b05b57bee1324&chksm=ced54965f9a2c073ba1badfedbc6610036455cd769a3c8ee3445f7fbff9364b5624091be9914&token=666852558&lang=zh_CN#rd)]

- 【文心一言新闻发布会内容复现】[[blog](https://mp.weixin.qq.com/s?__biz=Mzg3NDIyMzI0Mw==&mid=2247486081&idx=1&sn=034480a8b00778cb6a4f2b5ea4214974&chksm=ced54965f9a2c0733ff09fbff4953da484180f48545da3d9b476f1e7375c162f9e8d4eaa0afd&token=666852558&lang=zh_CN#rd)]

- 【GPT4 VS ChatGPT】[[blog](https://mp.weixin.qq.com/s?__biz=Mzg3NDIyMzI0Mw==&mid=2247485952&idx=2&sn=e54a62e358bf7aee3c007d59600fd452&chksm=ced549e4f9a2c0f2868eb8877c14fbe287a469e63b09774cefcb9edc4c0601016f6d36561973&token=666852558&lang=zh_CN#rd)]

## Text

### ChatGPT

![ChatGPT](images/chatgpt-head.png)

![ChatGPT_family](images/chatgpt-3.jpg)

- ### ChatGPT_Blogs
  - #### ChatGPT_Application

    - 【大模型时代的“Linux”生态，开启人工智能新十年】[[blog](https://mp.weixin.qq.com/s/sUmA3nSSVfNQFBgSjiSn0g)]
    - 【ChatGPT获得了「Wolfram」超能力】[[blog](https://writings.stephenwolfram.com/2023/03/chatgpt-gets-its-wolfram-superpowers/)]
    - 【OpenAI 将 ChatGPT 连接到互联网】[[blog](https://techcrunch.com/2023/03/23/openai-connects-chatgpt-to-the-internet/ )]
    - 【ChatAug：利用ChatGPT进行文本数据增强】[[paper](https://arxiv.org/abs/2302.13007 )]
    - 【ChatGPT产品潮来了：融入Slack、读PDF，创新不断】[[blog](https://mp.weixin.qq.com/s/S1DUJrNK5_H5krvHotOwHQ)]，[[试用地址](https://www.chatpdf.com/ )]
    - 【复旦大学教授肖仰华：ChatGPT 浪潮下，面向大模型如何做数据治理？】[[blog](https://mp.weixin.qq.com/s/od24PYvFLUJe4NQxjvsbMw)]
    - 【对话式AI搜索的技术路线猜想】[[blog](https://mp.weixin.qq.com/s/AIIu4rRi1WZRQn3oHtuwdg)]
    - 【ChatGPT 是数据隐私的另一个障碍吗】[[blog](https://www.bizcommunity.com/Article/196/639/236418.html)]

  - #### ChatGPT_Technology

    - #### [ChatGPT_Inference_Cost](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Inference_Cost.md)

    - #### [ChatGPT_Official_API_Learning](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Official_API_Learning.md)

    - #### [ChatGPT_Parameter_is_not_175B](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Parameter_is_not_175B.md)

    - #### [ChatGPT_Road_Map_from_yao.fu](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Road_Map_from_yao.fu.md)

    - #### [Lessons_Learned_from_ChatGPT_Recurrence](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/Lessons_Learned_from_ChatGPT_Recurrence.md)

    - #### [LLM_Pre-training_Guide（Bloom-175B）](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/LLM_Pre-training_Guide（Bloom-175B）.md)

    - #### [The_guide_of_training_LLM](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/The_guide_of_training_LLM.md)

    - 【AI芯片制造商Cerebras发布7个基于GPT的大语言模型，现已开源】[[官网地址](https://www.cerebras.net/blog/cerebras-gpt-a-family-of-open-compute-efficient-large-language-models/) )]，[[GPT地址](https://www.cerebras.net/cerebras-gpt  )]，[[Hugging Face地址 ](https://huggingface.co/cerebras  )]

    - 【大模型论文周报丨GPT-4发布，谷歌开放PaLM API，斯坦福7B开源模型Alpaca媲美GPT-3.5】[[blog](https://mp.weixin.qq.com/s/C6g_H6xfFn59IxnLpbjA1g)]

    - 【ChatGPT作者John Shulman：我们成功的秘密武器】[[blog](https://www.talkrl.com/episodes/john-schulman)]

  - #### ChatGPT_Other

    - [Cver](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/Cver.md)
    - [DataFun](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/DataFun.md)
    - [huggingface](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/huggingface.md)
    - [机器之心](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E6%9C%BA%E5%99%A8%E4%B9%8B%E5%BF%83.md)
    - [机器学习研究组订阅](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0%E7%A0%94%E7%A9%B6%E7%BB%84%E8%AE%A2%E9%98%85.md)
    - [机器学习算法与Python实战](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0%E7%AE%97%E6%B3%95%E4%B8%8EPython%E5%AE%9E%E6%88%98.md)
    - [量子位](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E9%87%8F%E5%AD%90%E4%BD%8D.md)
    - [NewBeeNLP](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/NewBeeNLP.md)
    - [PaperWeekly](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/PaperWeekly.md)
    - [图灵人工智能](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E5%9B%BE%E7%81%B5%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD.md)
    - [新智元](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E6%96%B0%E6%99%BA%E5%85%83.md)
    - [学术头条](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E5%AD%A6%E6%9C%AF%E5%A4%B4%E6%9D%A1.md)
    - [AI有道](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/AI%E6%9C%89%E9%81%93.md)
    - [智源社区](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E6%99%BA%E6%BA%90%E7%A4%BE%E5%8C%BA.md)
    - [专知](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/Other/%E4%B8%93%E7%9F%A5.md)
    - 【LLaMA模型Meta版泄露，GitHub获8K星】[[blog](https://mp.weixin.qq.com/s/2M19WSq2YICo-3t5ibQcig)]


- ### ChatGPT性能评估

- 【ChatGPT or Grammarly? Evaluating ChatGPT on Grammatical Error Correction Benchmark 】[[paper](https://arxiv.org/abs/2303.13648 )]

- 【用ChatGPT参加计算机科学考试】[[paper](https://arxiv.org/abs/2303.09461 )]

- 【探讨ChatGPT在对抗攻击和分布外泛化下的鲁棒性】[[paper](https://arxiv.org/pdf/2302.12095.pdf )]，[[code]([https://github.com/microsoft/robustlearn](https://github.com/wyu97/GenRead) )]


- ### ChatGPT_Papers


  - 【BloombergGPT: A Large Language Model for Finance】[[paper](https://papers.labml.ai/api/v1/redirect/pdf?paper_key=b0e4b03ecf5c11edb95839eec3084ddd)]
  - 【CodeGeeX: A Pre-Trained Model for Code Generation with Multilingual Evaluations on HumanEval-X 】[[paper](https://arxiv.org/pdf/2303.17568.pdf )]，[[code](https://github.com/THUDM/CodeGeeX )]
  - 【HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in HuggingFace 】[[paper](https://arxiv.org/pdf/2303.17580.pdf )]
  - 【ChatGPT is a Knowledgeable but Inexperienced Solver: An Investigation of Commonsense Problem in Large Language Models 】[[paper](https://arxiv.org/pdf/2303.16421.pdf )]
  - 【A Comprehensive Capability Analysis of GPT-3 and GPT-3.5 Series Models 】[[paper]([https://arxiv.org/abs/2303.10420v1 ](https://arxiv.org/abs/2303.10420v1%C2%A0) )]
  - 【ChatGPT Outperforms Crowd-Workers for Text-Annotation Tasks 】[[paper](https://arxiv.org/pdf/2303.15056.pdf )]
  - 【微软&佐治亚理工学院 | AdaLoRA：自适应预算分配以实现参数有效的微调】[[paper](https://arxiv.org/pdf/2303.10512.pdf )]，[[code](https://github.com/QingruZhang/AdaLoRA )]
  - 【微软 | 大型语言模型的语境忠实提示法】[[paper](https://arxiv.org/pdf/2303.11315.pdf )]
  - 【KAUST | ChatGPT问，BLIP-2回答模型：面向丰富的视觉描述的自动提问】[[paper](https://arxiv.org/pdf/2303.06594.pdf )]，[[code]([https://github.com/Vision-CAIR/ChatCaptioner](https://github.com/Vision-CAIR/) )]
  - 【微软 | 视觉 ChatGPT：使用视觉基础模型进行对话、绘图和编辑】[[paper](https://arxiv.org/pdf/2303.04671.pdf )]


### GPT4

- ### GPT4_Official
  - #### [GPT4_System_Card中文翻译](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Official/GPT-4_System_Card_zh.md)

  - #### [GPT4_Technical_Report中文翻译](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Official/GPT4_Technical_Report_zh.md)

- ### GPT4_Blogs
  - #### [GPT4技术细节](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Blog/GPT4_Technical_Detail.md)

  - #### [GPT4技术关键点总结](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Blog/GPT4_Technical_Summary.md)

  - #### [GPT4初衷](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Blog/Research_Origin_of_GPT-4.md)

  - #### [GPT4和ChatGPT的效果对比](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT_VS_GPT4/GPT4_VS_ChatGPT（from_nytimes）.md)

  - 【专访OpenAI 的联合创始人兼首席科学家：GPT-4 创造者 Ilya Sutskever 谈 AI 幻觉和 AI 民主】[[blog](https://www.forbes.com/sites/craigsmith/2023/03/15/gpt-4-creator-ilya-sutskever-on-ai-hallucinations-and-ai-democracy/?sh=7743f01e1218 )]

  - 【纽约时报：GPT-4 令人印象深刻但仍在 10 个方面具有缺陷】[[blog](https://www.nytimes.com/2023/03/14/technology/openai-new-gpt4.html)]

  - 【Open AI｜多模态大模型GPT-4的新突破】[[blog](https://hub.baai.ac.cn/view/24852)]

  - 【OpenAI ：重磅发布GPT-4】[[blog](https://openai.com/research/gpt-4)]

- ### GPT4_Papers
  - 【点燃通用人工智能的火花：GPT-4的早期实验】[[原始paper](https://arxiv.org/pdf/2303.12712.pdf )]，[[中文版paper](https://event-cdn.baai.ac.cn/file/file-browser/waTXJn85fm3FPyDXpsZ4faGk47trjjYb.pdf  )]
  - 【GPT4All：用GPT-3.5-Turbo的大规模数据提炼训练一个助理式聊天机器人】[[paper](https://s3.amazonaws.com/static.nomic.ai/gpt4all/2023_GPT4All_Technical_Report.pdf )]，[[code](https://github.com/nomic-ai/gpt4all )]
  - 【美国东北大学：可以通过要求GPT4反思“你为什么错了？”来提高30%的性能】[[paper](https://arxiv.org/abs/2303.11366 )]，[[code](https://github.com/noahshinn024/reflexion )]

### ChatGPT扩展模型

#### LLaMA以及扩展

- 【LLaMA】
- 【LLaMA评测】[[blog](https://mp.weixin.qq.com/s/kImwfWWtXMmEDVOhJZ4dJg)]
- 【Alpaca】
- 【LLaMA-Adapter】【**LLaMA-Adapter**，一种用于微调指令遵循[LLaMA](https://github.com/facebookresearch/llama)模型的轻量级自适应方法🔥[，使用Stanford Alpaca](https://github.com/tatsu-lab/stanford_alpaca)提供的 52K 数据。】[[paper](https://arxiv.org/pdf/2303.16199.pdf )]，[[code](https://github.com/ZrrSkywalker/LLaMA-Adapter )]
- 【lit-llama】【基于nanoGPT的LLaMA语言模型，支持量化、LoRA微调和预训练 】[[code](https://github.com/Lightning-AI/lit-llama)]
- 【Vicuna】【通过对从ShareGPT收集的用户共享对话进行微调的LLaMA训练，Vicuna-13B达到了OpenAI ChatGPT和Google Bard 90%*以上的质量 】[Vicuna官网地址](https://vicuna.lmsys.org/)

【ColossalAI】【完整复现ChatGPT全流程】[code](https://github.com/hpcaitech/ColossalAI)

【ColossalChat】【用于克隆 ChatGPT 和完整 RLHF 管道的开源解决方案】[[code](https: [//github.com/hpcaitech/ColossalAI](https://github.com/hpcaitech/ColossalAI) )]，[[blog](https://syncedreview.com/2023/03/29/colossalchat-an-open-source-solution-for-cloning-chatgpt-with-a-complete-rlhf-pipeline/)]

【Dolly**】【声称它 "**像ChatGPT一样神奇**"，但只需要**使用一台机器**在**不到三个小时的时间里**训练的数据少得多。】[[blog]([https://www.databricks.com/blog/2023/03/24/hello-dolly-democratizing-magic-chatgpt-open-models.html ](https://www.databricks.com/blog/2023/03/24/hello-dolly-democratizing-magic-chatgpt-open-models.html) )]，[[Databricks Inc地址 ]([https://www.databricks.com ](https://www.databricks.com%20/) )]

【FlexGen】【Meta & 斯坦福大学等：用单个GPU进行大型语言模型的高吞吐量生成性推理】[[paper](https://arxiv.org/pdf/2303.06865.pdf )]，[[code](https://github.com/FMInference/FlexGen )]

### Bard

- 【谷歌再次开放Bard访问权，向着ChatGPT发起再一次攻击】[[报名地址 ]([http://Bard.google.com](http://bard.google.com/) )]，[[blog](https://twitter.com/sundarpichai/status/1638180697352593408 )]，[[theverge](https://www.theverge.com/23649897/google-Bard-chatbot-search-engine)]

### Claude 

- 【ChatGPT最强竞品Claude今日开放API】[[产品地址 ]([https://www.anthropic.com/product](https://www.anthropic.com/product%C2%A0) )]，[[申请地址 ](https://www.anthropic.com/earlyaccess )]，[[API说明 ]([https://console.anthropic.com/docs/api ](https://console.anthropic.com/docs/api%C2%A0) )]

### ChatGLM

- 【ChatGLM：千亿基座的对话模型开启内测 ⸺对应单卡版本开源】[[blog](https://chatglm.cn/blog )]，[[code](https://github.com/THUDM/ChatGLM-6B.git )]

### ChatLLaMA

- 【初创公司 Nebuly AI在LLaMA基础上加入RLHF 开源 ChatLLaMA 训练方法】[[code](https://github.com/nebuly-ai/nebullvm/tree/main/apps/accelerate/chatllama )]

### OpenChatKit 

- 【ChatGPT开源平替OpenChatKit：参数量200亿，在4300万条指令上微调而成】[[blog](https://mp.weixin.qq.com/s/9Av3nhJLrcYAsBW9vVGjTw)]，[[code]([https://github.com/togethercomputer/OpenChatKit ](https://github.com/togethercomputer/OpenChatKit%C2%A0) )]，[[测试链接]([https://huggingface.co/spaces/togethercomputer/OpenChatKit ](https://huggingface.co/spaces/togethercomputer/OpenChatKit%C2%A0) )]，[[模型权重]([https://huggingface.co/togethercomputer/GPT-NeoXT-Chat-Base-20B ](https://huggingface.co/togethercomputer/GPT-NeoXT-Chat-Base-20B%C2%A0) )]，[[数据集](https://laion.ai/blog/oig-dataset/ )]

### LLM文本检测

- 【美国麻省大学&谷歌研究院：改写文本可以避开AI生成文本的检测器，但检索则是一种有效的防御】[[paper](https://papers.labml.ai/api/v1/redirect/pdf?paper_key=2cfe8cecc9f211edb95839eec3084ddd )]，[[code](https://github.com/martiansideofthemoon/ai-detection-paraphrases )]
- 【人工智能生成的文本能被可靠地检测出来吗？】[[paper](https://arxiv.org/pdf/2303.11156.pdf )]

## Picture&Video

### Picture&Video Blogs

- 【Genmo Chat】【这是一款创造性的copilot，使用GPT-4和一大套生成人工智能工具创建并编辑您需要的任何视频或图像。 】[[blog](https://www.genmo.ai/)]

- 【BlenderGPT】【**一款基于GPT-4的扩展程序BlenderGPT开源，这是一个由GPT3/4驱动的全能AI编辑助手，为Blender提供支持** 】[[code](https://github.com/gd3kr/BlenderGPT)]
- 【Firefly】【Adobe制造了一个人工智能图像生成器--并表示它没有窃取艺术家的作品来做这件事 】[[blog](https://www.theverge.com/2023/3/21/23648315/adobe-firefly-ai-image-generator-announced)]
- 【Bing Image Creator】【微软推出Bing Image Creator，用户可根据文本提示创建图片】[[blog](https://techcrunch.com/2023/03/21/microsoft-brings-openais-dall-e-image-creator-to-the-new-bing/ )]
- 【Hugging Face 现已支持使用达摩院text-to-video模型从文本生成视频】[[模型地址 ](https://modelscope.cn/models/damo/text-to-video-synthesis/summary )]

### Picture&Video Papers

- 【最新女娲大模型，中科院提出NUWA-XL：扩散模型中的扩散，生成超长视频】[[paper](https://arxiv.org/pdf/2303.12346.pdf )]，[[blog](https://msra-nuwa.azurewebsites.net/#/ )]
- 【艾伦AI研究院 & 华盛顿大学 | CHAMPAGNE：从大规模的网络视频中学习真实世界的对话】[[paper](https://arxiv.org/pdf/2303.09713.pdf )]，[[code](https://seungjuhan.me/champagne )]
- 【用AI直接复现你在想什么，Stable Diffusion逼真复现图像】[[paper](https://sites.google.com/view/stablediffusion-with-brain/ )]，[[blog](https://mp.weixin.qq.com/s/gIwj2eqNph8jHWOhYYEXIg)]

## Code

### Code Blogs



### Code Papers

- 【北京大学：具有大语言模型的自我规划代码生成】[[paper](https://arxiv.org/pdf/2303.06689.pdf )]

- 【MIT最新研究：利用大预言模型生成Code】[[paper](https://arxiv.org/abs/2303.05510 )]，[[code](https://github.com/shunzh/Code-AI-Tree-Search )]，[[项目网址](https://codeaimcts.github.io/ )]

- 【Baldur: 基于大型语言模型的完全证明生成与修复】[[paper](https://arxiv.org/abs/2303.04910 )]

- 【MathPrompter: 基于大型语言模型的数学推理】[[paper](https://arxiv.org/abs/2303.05398 )]

## Music

### Music Blogs



### Music Papers



## 关于我

**个人主页**：wshzd.github.io

**微信公众号**：

![公众号二维码](images/ArronAI.jpg)

## 声明

以上部分资料来自网络整理，供大家学习参考，如有侵权，麻烦联系我删除！ 

WeChat：h18821656387
