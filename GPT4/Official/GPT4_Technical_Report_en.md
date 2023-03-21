# GPT4_Technical_Report_en

Original link：https://openai.com/research/gpt-4

We’ve created GPT-4, the latest milestone in OpenAI’s effort in scaling up deep learning. GPT-4 is a large multimodal model (accepting image and text inputs, emitting text outputs) that, while less capable than humans in many real-world scenarios, exhibits human-level performance on various professional and academic benchmarks. 

We’ve created GPT-4, the latest milestone in OpenAI’s effort in scaling up deep learning. GPT-4 is a large multimodal model (accepting image and text inputs, emitting text outputs) that, while less capable than humans in many real-world scenarios, exhibits human-level performance on various professional and academic benchmarks. For example, it passes a simulated bar exam with a score around the top 10% of test takers; in contrast, GPT-3.5’s score was around the bottom 10%. We’ve spent 6 months iteratively [aligning](https://openai.com/research/instruction-following) GPT-4 using lessons from our adversarial testing program as well as ChatGPT, resulting in our best-ever results (though far from perfect) on factuality, steerability, and refusing to go outside of guardrails.

Over the past two years, we rebuilt our entire deep learning stack and, together with Azure, co-designed a supercomputer from the ground up for our workload. A year ago, we trained GPT-3.5 as a first “test run” of the system. We found and fixed some bugs and improved our theoretical foundations. As a result, our GPT-4 training run was (for us at least!) unprecedentedly stable, becoming our first large model whose training performance we were able to accurately predict ahead of time. As we continue to focus on reliable scaling, we aim to hone our methodology to help us predict and prepare for future capabilities increasingly far in advance—something we view as critical for safety.

We are releasing GPT-4’s text input capability via ChatGPT and the API (with a [waitlist](https://openai.com/waitlist/gpt-4-api)). To prepare the image input capability for wider availability, we’re collaborating closely with a [single partner](https://www.bemyeyes.com/) to start. We’re also open-sourcing [OpenAI Evals](https://github.com/openai/evals), our framework for automated evaluation of AI model performance, to allow anyone to report shortcomings in our models to help guide further improvements.

## Capabilities

In a casual conversation, the distinction between GPT-3.5 and GPT-4 can be subtle. The difference comes out when the complexity of the task reaches a sufficient threshold—GPT-4 is more reliable, creative, and able to handle much more nuanced instructions than GPT-3.5.

To understand the difference between the two models, we tested on a variety of benchmarks, including simulating exams that were originally designed for humans. We proceeded by using the most recent publicly-available tests (in the case of the Olympiads and AP free response questions) or by purchasing 2022–2023 editions of practice exams. We did no specific training for these exams. A minority of the problems in the exams were seen by the model during training, but we believe the results to be representative—see our [technical report](https://arxiv.org/abs/2303.08774) for details.

internal reference [1](https://openai.com/research/gpt-4#fn-1)

AP Calculus BCAMC 12Codeforces RatingAP English LiteratureAMC 10Uniform Bar ExamAP English LanguageAP ChemistryGRE QuantitativeAP Physics 2USABO Semifinal 2020AP MacroeconomicsAP StatisticsLSATGRE WritingAP MicroeconomicsAP BiologyGRE VerbalAP World HistorySAT MathAP US HistoryAP US GovernmentAP PsychologyAP Art HistorySAT EBRWAP Environmental ScienceExam0%20%40%60%80%100%Estimated percentile lower bound (among test takers)Exam results (ordered by GPT-3.5 performance)gpt-4gpt-4 (no vision)gpt3.5

| Simulated exams                                              | GPT-4estimated percentile | GPT-4 (no vision)estimated percentile | GPT-3.5estimated percentile |
| ------------------------------------------------------------ | ------------------------- | ------------------------------------- | --------------------------- |
| Uniform Bar Exam (MBE+MEE+MPT)[1](https://openai.com/research/gpt-4#fn-1) | 298 / 400~90th            | 298 / 400~90th                        | 213 / 400~10th              |
| LSAT                                                         | 163~88th                  | 161~83rd                              | 149~40th                    |
| SAT Evidence-Based Reading & Writing                         | 710 / 800~93rd            | 710 / 800~93rd                        | 670 / 800~87th              |
| SAT Math                                                     | 700 / 800~89th            | 690 / 800~89th                        | 590 / 800~70th              |
| Graduate Record Examination (GRE) Quantitative               | 163 / 170~80th            | 157 / 170~62nd                        | 147 / 170~25th              |
| Graduate Record Examination (GRE) Verbal                     | 169 / 170~99th            | 165 / 170~96th                        | 154 / 170~63rd              |
| Graduate Record Examination (GRE) Writing                    | 4 / 6~54th                | 4 / 6~54th                            | 4 / 6~54th                  |
| USABO Semifinal Exam 2020                                    | 87 / 15099th–100th        | 87 / 15099th–100th                    | 43 / 15031st–33rd           |
| USNCO Local Section Exam 2022                                | 36 / 60                   | 38 / 60                               | 24 / 60                     |
| Medical Knowledge Self-Assessment Program                    | 75%                       | 75%                                   | 53%                         |
| Codeforces Rating                                            | 392below 5th              | 392below 5th                          | 260below 5th                |
| AP Art History                                               | 586th–100th               | 586th–100th                           | 586th–100th                 |
| AP Biology                                                   | 585th–100th               | 585th–100th                           | 462nd–85th                  |
| AP Calculus BC                                               | 443rd–59th                | 443rd–59th                            | 10th–7th                    |

 We also evaluated GPT-4 on traditional benchmarks designed for machine learning models. GPT-4 considerably outperforms existing large language models, alongside most state-of-the-art (SOTA) models which may include benchmark-specific crafting or additional training protocols:

| Benchmark                                                    | GPT-4Evaluated few-shot | GPT-3.5Evaluated few-shot | LM SOTABest external LM evaluated few-shot                   | SOTABest external model (includes benchmark-specific training) |
| ------------------------------------------------------------ | ----------------------- | ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [MMLU](https://github.com/hendrycks/test)Multiple-choice questions in 57 subjects (professional & academic) | 86.4%5-shot             | 70.0%5-shot               | 70.7%[5-shot U-PaLM](https://arxiv.org/abs/2210.11399)       | 75.2%[5-shot Flan-PaLM](https://arxiv.org/abs/2210.11416)    |
| [HellaSwag](https://github.com/rowanz/hellaswag)Commonsense reasoning around everyday events | 95.3%10-shot            | 85.5%10-shot              | 84.2%[LLAMA (validation set)](https://arxiv.org/abs/2302.13971) | 85.6%[ALUM](https://arxiv.org/abs/2004.08994)                |
| [AI2 Reasoning Challenge (ARC)](https://leaderboard.allenai.org/arc/submissions/about)Grade-school multiple choice science questions. Challenge-set. | 96.3%25-shot            | 85.2%25-shot              | 84.2%[8-shot PaLM](https://arxiv.org/abs/2203.11171)         | 85.6%[ST-MOE](https://arxiv.org/abs/2202.08906)              |
| [WinoGrande](https://github.com/allenai/winogrande)Commonsense reasoning around pronoun resolution | 87.5%5-shot             | 81.6%5-shot               | 84.2%[5-shot PALM](https://arxiv.org/abs/2204.02311)         | 85.6%[5-shot PALM](https://arxiv.org/abs/2204.02311)         |
| [HumanEval](https://github.com/openai/human-eval)Python coding tasks | 67.0%0-shot             | 48.1%0-shot               | 26.2%[0-shot PaLM](https://arxiv.org/abs/2204.02311)         | 65.8%[CodeT + GPT-3.5](https://arxiv.org/abs/2207.10397v2)   |
| [DROP](https://arxiv.org/abs/1903.00161) (f1 score)Reading comprehension & arithmetic. | 80.93-shot              | 64.13-shot                | 70.8[1-shot PaLM](https://arxiv.org/abs/2204.02311)          | 88.4[QDGAT](https://arxiv.org/abs/2009.07448v1)              |

Many existing ML benchmarks are written in English. To get an initial sense of capability in other languages, we translated the MMLU benchmark—a suite of 14,000 multiple-choice problems spanning 57 subjects—into a variety of languages using Azure Translate (see [Appendix](https://openai.com/research/gpt-4#appendix)). In the 24 of 26 languages tested, GPT-4 outperforms the English-language performance of GPT-3.5 and other LLMs (Chinchilla, PaLM), including for low-resource languages such as Latvian, Welsh, and Swahili:

0%10%20%30%40%50%60%70%80%90%Accuracy →GPT-4 3-shot accuracy on MMLU across languagesRandomChinchillaPaLMgpt-3.5gpt-425.0%67.0%69.3%70.1%85.5%84.1%84.1%84.0%83.7%83.6%83.1%82.7%82.1%81.9%81.4%80.9%80.1%80.0%80.0%79.9%78.5%77.5%77.0%76.5%73.2%72.6%72.2%71.8%71.4%66.7%62.0%Random guessingChinchilla-EnglishPaLM-EnglishGPT-3.5-EnglishGPT-4 EnglishItalianAfrikaansSpanishGermanFrenchIndonesianRussianPolishUkranianGreekLatvianMandarinArabicTurkishJapaneseSwahiliWelshKoreanIcelandicBengaliUrduNepaliThaiPunjabiMarathiTelugu

We’ve also been using GPT-4 internally, with great impact on functions like support, sales, content moderation, and programming. We also are using it to assist humans in evaluating AI outputs, starting the second phase in our [alignment strategy](https://openai.com/blog/our-approach-to-alignment-research).

### Visual inputs

GPT-4 can accept a prompt of text and images, which—parallel to the text-only setting—lets the user specify any vision or language task. Specifically, it generates text outputs (natural language, code, etc.) given inputs consisting of interspersed text and images. Over a range of domains—including documents with text and photographs, diagrams, or screenshots—GPT-4 exhibits similar capabilities as it does on text-only inputs. Furthermore, it can be augmented with test-time techniques that were developed for text-only language models, including few-shot and [chain-of-thought](https://arxiv.org/abs/2201.11903) prompting. Image inputs are still a research preview and not publicly available.

User

What is funny about this image? Describe it panel by panel.

![message-0-attachment-0](https://cdn.openai.com/gpt-4/gpt-v-samples/vga.jpg)

Source: [hmmm (Reddit)](https://www.reddit.com/r/hmmm/comments/ubab5v/hmmm/)

GPT-4

The image shows a package for a "Lightning Cable" adapter with three panels.
Panel 1: A smartphone with a VGA connector (a large, blue, 15-pin connector typically used for computer monitors) plugged into its charging port.
Panel 2: The package for the "Lightning Cable" adapter with a picture of a VGA connector on it.
Panel 3: A close-up of the VGA connector with a small Lightning connector (used for charging iPhones and other Apple devices) at the end.
The humor in this image comes from the absurdity of plugging a large, outdated VGA connector into a small, modern smartphone charging port.

We preview GPT-4’s performance by evaluating it on a narrow suite of standard academic vision benchmarks. However, these numbers do not fully represent the extent of its capabilities as we are constantly discovering new and exciting tasks that the model is able to tackle. We plan to release further analyses and evaluation numbers as well as thorough investigation of the effect of test-time techniques soon.

internal footnote[A](https://openai.com/research/gpt-4#fn-A)[A]

We evaluate this benchmark using Chain-Of-Thought prompting with 4 examples from the training set in-context. The specific prompt was tuned on the validation set.

 

| Benchmark                                                    | GPT-4Evaluated few-shot                          | Few-shot SOTA                                                | SOTABest external model (includes benchmark-specific training) |
| ------------------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [VQAv2](https://arxiv.org/abs/1612.00837)VQA score (test-dev) | 77.2%0-shot                                      | 67.6%[Flamingo 32-shot](https://arxiv.org/abs/2204.14198)    | 84.3%[PaLI-17B](https://arxiv.org/abs/2209.06794)            |
| [TextVQA](https://arxiv.org/abs/1904.08920)VQA score (val)   | 78.0%0-shot                                      | 37.9%[Flamingo 32-shot](https://arxiv.org/abs/2204.14198)    | 71.8%[PaLI-17B](https://arxiv.org/abs/2209.06794)            |
| [ChartQA](https://arxiv.org/abs/2203.10244)Relaxed accuracy (test) | 78.5%[A](https://openai.com/research/gpt-4#fn-A) | -                                                            | 58.6%[Pix2Struct Large](https://arxiv.org/abs/2210.03347)    |
| [AI2 Diagram (AI2D)](https://arxiv.org/abs/1603.07396)Accuracy (test) | 78.2%0-shot                                      | -                                                            | 42.1%[Pix2Struct Large](https://arxiv.org/abs/2210.03347)    |
| [DocVQA](https://arxiv.org/abs/2007.00398)ANLS score (test)  | 88.4%0-shot (pixel-only)                         | -                                                            | 88.4%[ERNIE-Layout 2.0](https://arxiv.org/abs/2210.06155)    |
| [Infographic VQA](https://arxiv.org/abs/2104.12756)ANLS score (test) | 75.1%0-shot (pixel-only)                         | -                                                            | 61.2%[Applica.ai TILT](https://arxiv.org/abs/2102.09550)     |
| [TVQA](https://arxiv.org/abs/1809.01696)Accuracy (val)       | 87.3%0-shot                                      | -                                                            | 86.5%[MERLOT Reserve Large](https://arxiv.org/abs/2201.02639) |
| [LSMDC](https://arxiv.org/abs/1605.03705)Fill-in-the-blank accuracy (test) | 45.7%0-shot                                      | 31.0%[MERLOT Reserve 0-shot](https://arxiv.org/abs/2201.02639) | 52.9%[MERLOT](https://arxiv.org/abs/2106.02636)              |

### Steerability

We’ve been working on each aspect of the plan outlined in our post about [defining the behavior of AIs](https://openai.com/blog/how-should-ai-systems-behave), including steerability. Rather than the classic ChatGPT personality with a fixed verbosity, tone, and style, developers (and soon ChatGPT users) can now prescribe their AI’s style and task by describing those directions in the “system” message. System messages allow API users to significantly customize their users’ experience [within bounds](https://platform.openai.com/docs/usage-policies). We will keep making improvements here (and particularly know that system messages are the easiest way to “jailbreak” the current model, i.e., the adherence to the bounds is not perfect), but we encourage you to try it out and let us know what you think.

## Limitations

Despite its capabilities, GPT-4 has similar limitations as earlier GPT models. Most importantly, it still is not fully reliable (it “hallucinates” facts and makes reasoning errors). Great care should be taken when using language model outputs, particularly in high-stakes contexts, with the exact protocol (such as human review, grounding with additional context, or avoiding high-stakes uses altogether) matching the needs of a specific use-case.

While still a real issue, GPT-4 significantly reduces hallucinations relative to previous models (which have themselves been improving with each iteration). GPT-4 scores 40% higher than our latest GPT-3.5 on our internal adversarial factuality evaluations:

learningtechnologywritinghistorymathsciencerecommendationcodebusiness0%20%40%60%80%CategoryAccuracyInternal factual eval by categorychatgpt-v2chatgpt-v3chatgpt-v4gpt-4

On nine categories of internal adversarially-designed factual evals, we compare GPT-4 (green) to the first three ChatGPT versions. There are significant gains across all topics. An accuracy of 1.0 means the model’s answers are judged to be in agreement with human ideal responses for all questions in the eval.

We have made progress on external benchmarks like TruthfulQA, which tests the model’s ability to separate fact from an adversarially-selected set of incorrect statements. These questions are paired with factually incorrect answers that are statistically appealing.

Anthropic-LMAnthropic-LMgpt-3.5-basegpt-3.5-basegpt-3.5-turbogpt-4-basegpt-4-basegpt-40-shotRLHF0-shot5-shotRLHF0-shot5-shotRLHF0%10%20%30%40%50%60%70%ModelAccuracyAccuracy on adversarial questions (TruthfulQA mc1)Anthropic-LMgpt-3.5gpt-4

The GPT-4 base model is only slightly better at this task than GPT-3.5; however, after [RLHF](https://openai.com/research/learning-from-human-preferences) post-training (applying the same process we used with [GPT-3.5](https://openai.com/blog/chatgpt)) there is a large gap. Examining some examples below, GPT-4 resists selecting common sayings (you can’t teach an old dog new tricks), however it still can miss subtle details (Elvis Presley was not the son of an actor).

The model can have various biases in its outputs—we have made progress on these but there’s still more to do. Per our [recent blog post](https://openai.com/blog/how-should-ai-systems-behave), we aim to make AI systems we build have reasonable default behaviors that reflect a wide swathe of users’ values, allow those systems to be customized within broad bounds, and get public input on what those bounds should be.

GPT-4 generally lacks knowledge of events that have occurred after the vast majority of its data cuts off (September 2021), and does not learn from its experience. It can sometimes make simple reasoning errors which do not seem to comport with competence across so many domains, or be overly gullible in accepting obvious false statements from a user. And sometimes it can fail at hard problems the same way humans do, such as introducing security vulnerabilities into code it produces.

GPT-4 can also be confidently wrong in its predictions, not taking care to double-check work when it’s likely to make a mistake. Interestingly, the base pre-trained model is highly calibrated (its predicted confidence in an answer generally matches the probability of being correct). However, through our current post-training process, the calibration is reduced.

![Image6](https://openaicom.imgix.net/256ef0fb-5dca-4ae1-8318-d5bdbadeebb2/image6.png?fm=auto&auto=compress,format&fit=min&rect=0,0,480,446&w=3840&h=3568)

![Image3](https://openaicom.imgix.net/256ef0fb-5dca-4ae1-8318-d5bdbadeebb2/image3.png?fm=auto&auto=compress,format&fit=min&rect=0,0,676,634&w=3840&h=3601)

Left: Calibration plot of the pre-trained GPT-4 model on an MMLU subset. The model’s confidence in its prediction closely matches the probability of being correct. The dotted diagonal line represents perfect calibration. Right: Calibration plot of post-trained PPO GPT-4 model on the same MMLU subset. Our current process hurts the calibration quite a bit.

## Risks & mitigations

We’ve been iterating on GPT-4 to make it safer and more aligned from the beginning of training, with efforts including selection and filtering of the pretraining data, evaluations and expert engagement, model safety improvements, and monitoring and enforcement.

GPT-4 poses similar risks as previous models, such as generating harmful advice, buggy code, or inaccurate information. However, the additional capabilities of GPT-4 lead to new risk surfaces. To understand the extent of these risks, we engaged over 50 experts from domains such as AI alignment risks, cybersecurity, biorisk, trust and safety, and international security to adversarially test the model. Their findings specifically enabled us to test model behavior in high-risk areas which require expertise to evaluate. Feedback and data from these experts fed into our mitigations and improvements for the model; for example, we’ve collected additional data to improve GPT-4’s ability to refuse requests on how to synthesize dangerous chemicals.

GPT-4 incorporates an additional safety reward signal during RLHF training to reduce harmful outputs (as defined by our [usage guidelines](https://platform.openai.com/docs/usage-policies/disallowed-usage)) by training the model to refuse requests for such content. The reward is provided by a GPT-4 zero-shot classifier judging safety boundaries and completion style on safety-related prompts. To prevent the model from refusing valid requests, we collect a diverse dataset from various sources (e.g., labeled production data, human red-teaming, model-generated prompts) and apply the safety reward signal (with a positive or negative value) on both allowed and disallowed categories. 

Our mitigations have significantly improved many of GPT-4’s safety properties compared to GPT-3.5. We’ve decreased the model’s tendency to respond to requests for disallowed content by 82% compared to GPT-3.5, and GPT-4 responds to sensitive requests (e.g., medical advice and self-harm) in accordance with our policies 29% more often.

![1679367552881](C:\Users\zhidong.he\AppData\Local\Temp\1679367552881.png)



Overall, our model-level interventions increase the difficulty of eliciting bad behavior but doing so is still possible. Additionally, there still exist “jailbreaks” to generate content which violate our [usage guidelines](https://openai.com/policies/usage-policies). As the “risk per token” of AI systems increases, it will become critical to achieve extremely high degrees of reliability in these interventions; for now it’s important to complement these limitations with deployment-time safety techniques like monitoring for abuse.

GPT-4 and successor models have the potential to significantly influence society in both beneficial and harmful ways. We are collaborating with external researchers to improve how we understand and assess potential impacts, as well as to build evaluations for dangerous capabilities that may emerge in future systems. We will soon share more of our thinking on the potential social and economic impacts of GPT-4 and other AI systems.

## Training process

Like previous GPT models, the GPT-4 base model was trained to predict the next word in a document, and was trained using publicly available data (such as internet data) as well as data we’ve licensed. The data is a web-scale corpus of data including correct and incorrect solutions to math problems, weak and strong reasoning, self-contradictory and consistent statements, and representing a great variety of ideologies and ideas.

So when prompted with a question, the base model can respond in a wide variety of ways that might be far from a user’s intent. To align it with the user’s intent within guardrails, we fine-tune the model’s behavior using reinforcement learning with human feedback ([RLHF](https://openai.com/research/learning-from-human-preferences)).

Note that the model’s capabilities seem to come primarily from the pre-training process—RLHF does not improve exam performance (without active effort, it actually degrades it). But steering of the model comes from the post-training process—the base model requires prompt engineering to even know that it should answer the questions.

### Predictable scaling

A large focus of the GPT-4 project has been building a deep learning stack that scales predictably. The primary reason is that, for very large training runs like GPT-4, it is not feasible to do extensive model-specific tuning. We developed infrastructure and optimization that have very predictable behavior across multiple scales. To verify this scalability, we accurately predicted in advance GPT-4’s final loss on our internal codebase (not part of the training set) by extrapolating from models trained using the same methodology but using 10,000x less compute:

ObservedPredictiongpt-4100p10n1µ100µ0.011Compute1.02.03.04.05.06.0Bits per wordOpenAI codebase next word prediction

Now that we can accurately predict the metric we optimize during training (loss), we’re starting to develop methodology to predict more interpretable metrics. For example, we successfully predicted the pass rate on a subset of the [HumanEval](https://github.com/openai/human-eval) dataset, extrapolating from models with 1,000x less compute:

ObservedPredictiongpt-41µ10µ100µ0.0010.010.11Compute012345– Mean Log Pass RateCapability prediction on 23 coding problems

Some capabilities are still hard to predict. For example, the Inverse Scaling Prize was a competition to find a metric that gets worse as model compute increases, and [hindsight neglect](https://www.alignmentforum.org/posts/iznohbCPFkeB9kAJL/inverse-scaling-prize-round-1-winners#_The_Floating_Droid___for_hindsight_neglect_10shot) was one of the winners. Just like with another recent [result,](https://arxiv.org/abs/2211.02011) GPT-4 reverses the trend:

adababbagecuriegpt-3.5gpt-4Model020406080100AccuracyInverse scaling prize, hindsight neglect

We believe that accurately predicting future machine learning capabilities is an important part of safety that doesn’t get nearly enough attention relative to its potential impact (though we’ve been encouraged by efforts across several institutions). We are scaling up our efforts to develop methods that provide society with better guidance about what to expect from future systems, and we hope this becomes a common goal in the field.

## OpenAI Evals

We’re open-sourcing [OpenAI Evals](https://github.com/openai/evals), our software framework for creating and running benchmarks for evaluating models like GPT-4, while inspecting their performance sample by sample. We use Evals to guide development of our models (both identifying shortcomings and preventing regressions), and our users can apply it for tracking performance across model versions (which will now be coming out regularly) and evolving product integrations. For example, Stripe has used Evals to complement their human evaluations to measure the accuracy of their GPT-powered documentation tool.

Because the code is all open-source, Evals supports writing new classes to implement [custom evaluation logic](https://github.com/openai/evals/blob/main/docs/custom-eval.md). In our own experience, however, many benchmarks follow one of a few “templates,” so we have also [included the templates](https://github.com/openai/evals/blob/main/docs/eval-templates.md) that have been most useful internally (including a template for “model-graded evals”—we’ve found that GPT-4 is surprisingly capable of checking its own work). Generally the most effective way to [build a new eval](https://github.com/openai/evals/blob/main/docs/build-eval.md) will be to instantiate one of these templates along with providing data. We’re excited to see what others can build with these templates and with Evals more generally.

We are hoping Evals becomes a vehicle to share and crowdsource benchmarks, representing a maximally wide set of failure modes and difficult tasks. As an example to follow, we’ve created a [logic puzzles](https://github.com/openai/evals/blob/main/evals/registry/evals/logic.yaml) eval which contains ten prompts where GPT-4 fails. Evals is also compatible with implementing existing benchmarks; we’ve included several [notebooks](https://github.com/openai/evals/tree/main/examples) implementing academic benchmarks and a few variations of integrating (small subsets of) [CoQA](https://github.com/openai/evals/blob/main/evals/registry/evals/coqa-ex.yaml) as an example.

We invite everyone to use Evals to test our models and submit the most interesting examples.We believe that Evals will be an integral part of the process for using and building on top of our models, and we welcome [direct contributions, questions, and feedback](https://github.com/openai/evals).

## ChatGPT Plus

ChatGPT Plus subscribers will get GPT-4 access on chat.openai.com with a usage cap. We will adjust the exact usage cap depending on demand and system performance in practice, but we expect to be severely capacity constrained (though we will scale up and optimize over upcoming months).

Depending on the traffic patterns we see, we may introduce a new subscription level for higher-volume GPT-4 usage; we also hope at some point to offer some amount of free GPT-4 queries so those without a subscription can try it too.

## API

To get access to the GPT-4 API (which uses the same [ChatCompletions API](https://platform.openai.com/docs/guides/chat/chat-vs-completions) as gpt-3.5-turbo), please [sign up for our waitlist](https://openai.com/waitlist/gpt-4). We will start inviting some developers today, and scale up gradually to balance capacity with demand. If you are a researcher studying the societal impact of AI or AI alignment issues, you can also apply for subsidized access via our [Researcher Access Program](https://openai.com/form/researcher-access-program).

Once you have access, you can make text-only requests to the gpt-4 model (image inputs are still in limited alpha), which we will automatically update to our recommended stable model as we make new versions over time (you can pin the current version by calling gpt-4-0314, which we’ll support until June 14). Pricing is $0.03 per 1k prompt tokens and $0.06 per 1k completion tokens. Default rate limits are 40k tokens per minute and 200 requests per minute.

gpt-4 has a context length of 8,192 tokens. We are also providing limited access to our 32,768–context (about 50 pages of text) version, gpt-4-32k, which will also be updated automatically over time (current version gpt-4-32k-0314, also supported until June 14). Pricing is $0.06 per 1K prompt tokens and $0.12 per 1k completion tokens. We are still improving model quality for long context and would love feedback on how it performs for your use-case. We are processing requests for the 8K and 32K engines at different rates based on capacity, so you may receive access to them at different times.

## Conclusion

We look forward to GPT-4 becoming a valuable tool in improving people’s lives by powering many applications. There’s still a lot of work to do, and we look forward to improving this model through the collective efforts of the community building on top of, exploring, and contributing to the model.

For more: [Read paper](https://arxiv.org/abs/2303.08774) / [View system card](https://cdn.openai.com/papers/gpt-4-system-card.pdf) / [Try on ChatGPT Plus](https://chat.openai.com/chat) / [Join API waitlist](https://openai.com/waitlist/gpt-4-api) / [Rewatch demo livestream](https://youtube.com/live/outcGtbnMuQ?feature=share) / [Contribute to OpenAI Evals](https://github.com/openai/evals)