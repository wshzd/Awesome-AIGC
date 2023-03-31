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

- [通用人工智能AGI](#通用人工智能agi)

  - [通用人工智能AGI开源工具](#通用人工智能agi开源工具)

  - [通用人工智能AGI相关会议](#通用人工智能agi相关会议)

  - [通用人工智能AGI相关博客及论文](#通用人工智能agi相关博客及论文)
- [AIGC相关会议](aigc相关会议)
- [文本生成](#文本生成)

  - [ChatGPT](#chatgpt)
    - [ChatGPT_Blogs](#chatgpt_blogs)
      - [ChatGPT_Application](#chatgpt_application)
      - [ChatGPT_Technology](#chatgpt_technology)
      - [ChatGPT_Other](#chatgpt_other)
    - [ChatGPT测试体验](#chatgpt测试体验)
    - [ChatGPT性能评估](#chatgpt性能评估)
    - [ChatGPT_Papers](#chatgpt_papers)
  - [GPT4](#gpt4)
    - [GPT4_Official](#gpt4_official)
    - [GPT4_System_Card_zh](#gpt4_system_card_zh)

    - [GPT4_Technical_Report_zh](#gpt4_technical_report_zh)

    - [GPT4_Blogs](#gpt4_blogs)
      - [GPT4_Technical_Detail](#gpt4_technical_detail)
      - [GPT4_Technical_Summary](#gpt4_technical_summary)
      - [Research Origin of GPT4](#research_origin_of_gpt4)

    - [GPT4_Papers](#gpt4_papers)
      - [GPT4 Papers](#gpt4_papers)
  - [ChatGPT扩展模型](#chatgpt扩展模型)
    - [LLaMA以及扩展](#LLaMA以及扩展)
    - [ColossalAI](#colossalai)
    - 
    - 
- [图像、视频生成](#图像、视频生成)



- [代码生成](#代码生成)



- [音乐生成](#音乐生成)





## 通用人工智能AGI

- ### 通用人工智能AGI开源工具

  - ### [Google发布统计深度学习框架平台：OpenXLA](https://github.com/wshzd/ChatGPT-Summary/blob/main/AGI/Google_OpenXLA.md)

- ### 通用人工智能AGI相关会议

- ### 通用人工智能AGI相关博客及论文

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


- ### [OpenAI团队介绍](https://github.com/wshzd/ChatGPT-Summary/blob/main/AGI/OpenAI_Team.md)


- ### [OpenAI的AGI路线图](https://github.com/wshzd/ChatGPT-Summary/blob/main/AGI/OpenAI发布AGI路线图.md)

## AIGC相关会议



## 文本生成

### ChatGPT

![ChatGPT](images/chatgpt-head.png)

![ChatGPT_family](images/chatgpt-3.jpg)

- ### ChatGPT_Blogs
  - #### ChatGPT_Application

    - 【大模型时代的“Linux”生态，开启人工智能新十年】[[blog](https://mp.weixin.qq.com/s/sUmA3nSSVfNQFBgSjiSn0g)]

  - #### ChatGPT_Technology

    - #### [ChatGPT_Inference_Cost](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Inference_Cost.md)

    - #### [ChatGPT_Official_API_Learning](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Official_API_Learning.md)

    - #### [ChatGPT_Parameter_is_not_175B](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Parameter_is_not_175B.md)

    - #### [ChatGPT_Road_Map_from_yao.fu](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/ChatGPT_Road_Map_from_yao.fu.md)

    - #### [Lessons_Learned_from_ChatGPT_Recurrence](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/Lessons_Learned_from_ChatGPT_Recurrence.md)

    - #### [LLM_Emergent_Ability](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/LLM_Emergent_Ability.md)

    - #### [LLM_Pre-training_Guide（Bloom-175B）](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/LLM_Pre-training_Guide（Bloom-175B）.md)

    - #### [The_guide_of_training_LLM](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT/Blog/ChatGPT_Technology/The_guide_of_training_LLM.md)

    - 【AI芯片制造商Cerebras发布7个基于GPT的大语言模型，现已开源】[[官网地址]([https://www.cerebras.net/blog/cerebras-gpt-a-family-of-open-compute-efficient-large-language-models](https://www.cerebras.net/blog/cerebras-gpt-a-family-of-open-compute-efficient-large-language-models/) )]，[[GPT地址](https://www.cerebras.net/cerebras-gpt  )]，[[Hugging Face地址 ](https://huggingface.co/cerebras  )]

    - 

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

- ### ChatGPT测试体验


- ### ChatGPT性能评估


- ### ChatGPT_Papers


  - 【BloombergGPT: A Large Language Model for Finance】[[paper](https://papers.labml.ai/api/v1/redirect/pdf?paper_key=b0e4b03ecf5c11edb95839eec3084ddd)]
  - 【CodeGeeX: A Pre-Trained Model for Code Generation with Multilingual Evaluations on HumanEval-X 】[[paper](https://arxiv.org/pdf/2303.17568.pdf )]，[[code](https://github.com/THUDM/CodeGeeX )]
  - 【HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in HuggingFace 】[[paper](https://arxiv.org/pdf/2303.17580.pdf )]
  - 【ChatGPT is a Knowledgeable but Inexperienced Solver: An Investigation of Commonsense Problem in Large Language Models 】[[paper](https://arxiv.org/pdf/2303.16421.pdf )]
  - 【A Comprehensive Capability Analysis of GPT-3 and GPT-3.5 Series Models 】[[paper]([https://arxiv.org/abs/2303.10420v1 ](https://arxiv.org/abs/2303.10420v1%C2%A0) )]
  - 【ChatGPT Outperforms Crowd-Workers for Text-Annotation Tasks 】[[paper](https://arxiv.org/pdf/2303.15056.pdf )]


### GPT4

- ### GPT4_Official
  - #### [GPT4_System_Card中文翻译](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Official/GPT-4_System_Card_zh.md)

  - #### [GPT4_Technical_Report中文翻译](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Official/GPT4_Technical_Report_zh.md)

- ### GPT4_Blogs
  - #### [GPT4技术细节](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Blog/GPT4_Technical_Detail.md)

  - #### [GPT4技术关键点总结](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Blog/GPT4_Technical_Summary.md)

  - #### [GPT4初衷](https://github.com/wshzd/ChatGPT-Summary/blob/main/GPT4/Blog/Research_Origin_of_GPT-4.md)

  - #### [GPT4和ChatGPT的效果对比](https://github.com/wshzd/ChatGPT-Summary/blob/main/ChatGPT_VS_GPT4/GPT4_VS_ChatGPT（from_nytimes）.md)

- ### GPT4_Papers
  - 【点燃通用人工智能的火花：GPT-4的早期实验】[[原始paper](https://arxiv.org/pdf/2303.12712.pdf )]，[[中文版paper](https://event-cdn.baai.ac.cn/file/file-browser/waTXJn85fm3FPyDXpsZ4faGk47trjjYb.pdf  )]
  - 【GPT4All：用GPT-3.5-Turbo的大规模数据提炼训练一个助理式聊天机器人】[[paper](https://s3.amazonaws.com/static.nomic.ai/gpt4all/2023_GPT4All_Technical_Report.pdf )]，[[code](https://github.com/nomic-ai/gpt4all )]

### ChatGPT扩展模型

#### LLaMA以及扩展

- 【LLaMA】
- 【Alpaca】
- 【LLaMA-Adapter】【**LLaMA-Adapter**，一种用于微调指令遵循[LLaMA](https://github.com/facebookresearch/llama)模型的轻量级自适应方法🔥[，使用Stanford Alpaca](https://github.com/tatsu-lab/stanford_alpaca)提供的 52K 数据。】[[paper](https://arxiv.org/pdf/2303.16199.pdf )]，[[code](https://github.com/ZrrSkywalker/LLaMA-Adapter )]
- 【lit-llama】【基于nanoGPT的LLaMA语言模型，支持量化、LoRA微调和预训练 】[[code](https://github.com/Lightning-AI/lit-llama)]
- 【Vicuna】【通过对从ShareGPT收集的用户共享对话进行微调的LLaMA训练，Vicuna-13B达到了OpenAI ChatGPT和Google Bard 90%*以上的质量 】[Vicuna官网地址](https://vicuna.lmsys.org/)

【ColossalAI】【完整复现ChatGPT全流程】[code](https://github.com/hpcaitech/ColossalAI)

【ColossalChat】【用于克隆 ChatGPT 和完整 RLHF 管道的开源解决方案】[[code](https: [//github.com/hpcaitech/ColossalAI](https://github.com/hpcaitech/ColossalAI) )]，[[blog](https://syncedreview.com/2023/03/29/colossalchat-an-open-source-solution-for-cloning-chatgpt-with-a-complete-rlhf-pipeline/)]

## 图像、视频生成

【Genmo Chat】【这是一款创造性的copilot，使用GPT-4和一大套生成人工智能工具创建并编辑您需要的任何视频或图像。 】[[blog](https://www.genmo.ai/)]

## 代码生成



## 音乐生成





## 关于我

**个人主页**：wshzd.github.io

**微信公众号**：

![公众号二维码](images/ArronAI.jpg)

## 声明

以上部分资料来自网络整理，供大家学习参考，如有侵权，麻烦联系我删除！ 

WeChat：h18821656387
