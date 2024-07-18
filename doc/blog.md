# 第一次越狱
# LLM Jailbreak Attack versus Defense Techniques - A Comprehensive Study
## 摘要
大型语言模型（LLM）已经越来越成为生成具有潜在社会影响的内容的核心。值得注意的是，这些模型已经展示了生成可能被认为是有害的内容的能力。为了减轻这些风险，研究人员采用了安全培训技术，将模型输出社会价值观保持一致，以遏制恶意内容的产生。然而，“越狱”现象——精心制作的提示会引发模型中的有害反应——仍然是一个重大挑战。研究对现有的关于越狱LLM及其防御技术的研究进行了综合分析。我们细致地研究了9种攻击技术和7种防御技术，它们应用于三种不同的语言模型： Vicuna，LLama，和GPT-3.5 Turbo。我们的目的是评估这些攻击和防御技术的有效性。我们的研究结果显示，与通用技术相比，现有的白盒攻击表现不佳，并且在输入中包含特殊标记会显著影响攻击成功的可能性。本研究强调了重点关注LLM的安全方面的必要性。此外，我们通过发布我们的数据集和测试框架，为该领域做出了贡献，旨在促进对LLM安全性的进一步研究。我们相信，这些贡献将有助于探索这一领域内的安全措施。

## Q：这篇论文试图解决什么问题？ 
A: 尽管有各种各样的越狱攻击和防御方法，但仍然缺少关于越狱攻击在防御机制下的表现以及防御机制在越狱攻击下的表现的全面评估。该研究旨在回答两个关键的研究问题。RQ1：越狱攻击的有效性。RQ2：越狱防御的有效性。

## Q：如何解决这些问题？概述
![image.png](/doc/image/1.png)

## 攻击模型分类
Generative Techniques
<br>Template Techniques
<br>Training Gaps Techniques
![image.png](/doc/image/18.png)

## 防御模型分类
Self-Processing Defenses（自我防御）<br>Additional Helper Defenses（借助辅助LLM验证）<br>Input Permutation Defenses（输入排列）
![image.png](/doc/image/19.png)
## 实验设计
### Baseline Selection
RQ1:面向五种Generative Techniques(AutoDAN, PAIR, TAP, GPTFuzz, GCG)（动态生成，避开防御）
<br>四种Template Techniques (Jailbroken , 77 Templates from existing study, Deep Inception, Parameters )
<br>RQ2:面向四种防御策略Bergeron (Pisano) for additional helper methods;
<br>RALLM  and SmoothLLM  for input permutation
<br>techniques; and Baseline for perplexity analysis.

### Benchmark Construction
利用了Liu等人提出的基准测试框架，为了增强我们的评估的鲁棒性，我们扩展了原始数据集，以包括60个恶意查询，有效地将其规模增加了一倍。（数据集扩展方法严格遵循了以往研究中建立的分类和选择标准，确保了增强的数据集进行综合评估的一致性和相关性）

### Result Labeling
难点:手工审查的不切实际和缺乏恶意反应的标准化评估方法<br>
现有策略：Zou等人利用一组常见的拒绝模式，如“对不起”和“我不能”，来自动识别不符合要求的响应。Yu等人和Huang等人分别专注于增强机器学习模型，特别是RoBERTa和BERT-BASE-CASED的模型。此外，Chao等人还探索了利用GPT-4进行攻击分析的方法。<br>
该文章的新策略：利用手动注释的dataset细化RoBERTa模型
![image.png](/doc/image/4.png)<br>

### Evalution
RQ1:ASR（ Attack Success Rate）+efficiency<br>
RQ2:DPR（Defense Passing Rate）+BPR（ Attack Success Rate）+CRQ(Generated Response Quality)<br>
-多个评估点保证评估准确性
## 实验结果
越狱防御的有效性<br>
![image.png](/doc/image/2.png)<br>
越狱攻击的有效性<br>
![image.png](/doc/image/3.png)

## 对于实验结果的讨论
与通用技术相比，现有的白盒攻击表现不佳，并且在输入中包含特殊标记会显著影响攻击成功的可能性。eg：在输入中加入special tokens ‘[/INST]’能提高对LLama的攻击成功率
![image.png](/doc/image/20.png)
## 有什么可以进一步探索的点？
-在本研究中进行的综合分析的结果基础上，实施更强大的防御机制，以增强大型语言模型（LLM）的安全性并防范越狱攻击 <br>
-进一步探索和开发创新攻击技术和增强防御策略，查找LLM中的潜在威胁和漏洞。<br>
-调查不同类型的提示和输入对模型越狱敏感性的影响，特别是与通用技术对抗白盒攻击的有效性相关的影响 <br>
-对本文中提出的数据集、测试框架和方法进行测评和验证，以促进LLM安全研究的可重复性 <br>

# Jailbreaking ChatGPT via Prompt Engineering: An Empirical Study
## 摘要
像 CHATGPT 这样的大型语言模型 (LLM) 已显示出巨大的潜力，但也存在内容限制和潜在滥用等挑战。 -该研究侧重于三个主要的研究问题： 1.识别可以避开 LLM 限制的不同类型的提示。 2.评估这些越狱提示在避开 LLM 限制方面的有效性。 3.研究 CHATGPT 能否承受这些越狱提示。 -最初，研究人员创建了一个模型来对现有提示进行分类，发现了十种不同的模式和三类越狱提示。 -然后，他们使用CHATGPT 3.5和4.0版本测试了提示的越狱能力，分析了禁止某些内容的八个场景中的3,120个越狱问题。 -该研究发现，CHATGPT可以在40种不同场景中持续绕过限制，这突显了提示结构在绕过LLM限制方面的重要性。 -该研究还讨论了与创建和防止强大的越狱提示相关的挑战。
## Q：这篇论文试图解决什么问题？
RQ1:有多少种提示类型可以破解llm？<br>
RQ2:越狱提示如何绕过llm的限制？<br>
RQ3:CHATGPT对越狱提示的保护强度如何？

## 怎么解决这些问题？-实验过程以及发现
1.提示数据的收集<br>
2.将越狱提示分类<br>
![image.png](/doc/image/5.png)<br>
![image.png](/doc/image/8.png)<br>
发现：最常见的越狱提示类型是pretend，这是一种有效的越狱方案。更复杂的提示不太可能发生在现实世界的越狱中，因为它们需要更高水平的领域知识和复杂性。<br>
3.生成场景
![image.png](/doc/image/7.png)<br>
4.比较不同越狱类型在不同场景下的成功率<br>
![image.png](/doc/image/6.png)<br>
发现：IA、FDA和ADULT是最容易被越狱的情况，SIMU和SUPER是越狱提示中最有效的模式。RE和SIMU在越狱方面表现出更好的鲁棒性，LOGIC和PROG具有最差的鲁棒性。<br>
5.比较GPT-3.5-TURBO与GPT-4的成功案例<br>
![image.png](/doc/image/9.png)<br>
发现：与GPT-3.5 TURBO相比,GPT-4对提取禁止内容的越狱提示表现出更大的抵抗力。<br>
6.比较越狱与非越狱提示的成功率<br>
![image.png](/doc/image/10.png)<br>
发现：越狱提示明显优于非越狱提示。然而，在某些情况下，非越狱提示与越狱提示的效果同样好。这表明，由OpenAI实现的限制可能不够强大，无法防止在所有场景中使用被禁止内容。

## 研究论文的局限性
-范围有限： -本文专门分析CHATGPT版本3.5和4.0的越狱提示，这可能无法完全代表所有LLM的挑战范围 <br>
-数据集大小： -该研究使用了包含3,120个越狱问题的数据集，该数据集虽然丰富，但可能无法涵盖所有潜在的越狱提示和场景，这表明需要更大、更多样化的数据集进行全面分析。<br>
-可推广性： -这些发现可能仅限于所有LLM，因为该研究主要集中在CHATGPT上，而且越狱提示的有效性可能因不同的语言模型和平台而异。

## 有什么可以进一步探索的点？
-设计更强大的狱刑提示：为了绕过大型语言模型的限制，可以研究如何构造更加巧妙和难以检测的狱刑提示。<br>
-越狱攻击的预防和检测：开发有效的防御机制来防止提示工程攻击，例如，建立模型能够识别并阻止狱刑提示的机制，或者增强模型的自我意识，使其能辨别虚拟场景和现实世界之间的界限。<br>
-开源LLMs的越狱攻击情况：由于ChatGPT不是唯一的大型语言模型，因此对于像LLaMA这样的开源模型，了解它们对越狱提示的敏感性和抵抗力也很重要，这有助于社区制定相应的安全策略。<br>

# Jailbroken: How Does LLM Safety Training Fail?
## 摘要
经过安全和无害培训的大型语言模型仍然容易受到对抗性误用，对早期发布的ChatGPT的“越狱”攻击普遍存在，从而引发不希望的行为。认识到这个问题后，我们调查为什么这样的攻击能够成功，以及如何创建它们。我们假设了安全训练的两种失效模式：相互竞争目标和不匹配的泛化。当模型的能力和安全目标发生冲突时，就会出现相互竞争的目标，而当安全培训未能泛化到模型的有些领域时，就会出现不匹配的泛化。我们使用这些失败模式来指导越狱设计，然后评估最先进的模型，包括 OpenAI’s GPT-4 和 Anthropic’s Claude v1.3，以对抗现有的和新设计的攻击。我们发现，尽管这些模型背后进行了大量的red-teaming（模拟真实攻击完善模型） 和 safety-training的努力，漏洞仍然存在。值得注意的是，利用我们的失败模式的新攻击在来自模型的red-teaming评估集的不安全请求集合中的每个提示上都是成功的，并优于现有的特别越狱。我们的分析强调了安全-能力对等的必要性——安全机制应该和底层模型一样复杂——并反对单仅仅扩大规模就可以解决这些安全故障模式的观点。
![image.png](/doc/image/11.png)<br>
## 越狱模型分类：Competing Objectives相互竞争目标和Mismatched Generalization不匹配的泛化
当一个模型的预训练和监督学习SL遵循目标与其安全目标不一致时，就会出现竞争目标。<br>
不匹配的泛化是模型的安全培训数据输入未能推广到与模型能力训练的语料库数据一致时发生
## Competing Objectives
Example: Prefix Injection前缀注入<br>
![image.png](/doc/image/12.png)<br>
Example: Refusal Suppression拒绝抑制<br>
![image.png](/doc/image/13.png)<br>
一旦响应开始，训练前的目标非常倾向于继续，而不是突然逆转，从而导致完全不安全的输出<br>
## Mismatched Generalization
Example: Base64基于二进制到文本的编码方式
![image.png](/doc/image/14.png)<br>
不匹配的泛化可能发生是因为大型模型（如GPT-4和Claude v1.3）在预训练过程中选择了Base64，并学习直接遵循Base64编码的指令。但另一方面，safety training也很可能不包含像base64编码的指令那样不自然的输入，因此该模型从未被训练过拒绝这些提示的输入。因此，由于输入远远超出训练分布，模型没有被拒绝响应是合理的。<br>
Other examples：ROT13密码、火星文（用视觉上相似的数字和符号替换字母）和莫尔斯电码，用同义词取代敏感词（例如，“pilfer”而不是“steal”），将敏感单词分割成子字符串。
## Empirical Evaluation of Jailbreak Methods越狱方法的实验评估
-Baseline基线测试：进行了对照测试，其中使用了非越狱方法，逐字回应了每个提示以进行比较
-评估结果![image.png](/doc/image/16.png)<br>
攻击类型：Combination attacks，Model-assisted attacks，Jailbreakchat.com，Adversarial system prompt（对抗性），Adaptive attack（利用模型漏洞-最大可能性解码）<br>
结果分析：注入的特定前缀和特定的指令对于这些越狱的成功很重要。<br>
自适应攻击的有效性。<br>
规模扩大带来漏洞。<br>
![image.png](/doc/image/17.png)<br>
## 有什么可以进一步探索的点？
-未来的研究可能侧重于了解safety training在技术层面上的运作方式，并探索更高级的越狱攻击，同时完全了解该模型的内部工作原理。<br>
-探讨是否可以对safety training的结果进行机械解释，并研究设计出具有白盒访问权限的更强大越狱的可能性<br>


# 为什么LLM在对话中会出现混乱的情况（前后回答不一致）
论文标题：                                 
Ask Again, Then Fail: Large Language Models' Vacillations in Judgement<br>
论文地址：<br>
https://arxiv.org/abs/2310.02174​​<br>
项目网站：<br>
​​https://github.com/NUSTM/LLMs-Waver-In-Judgements​​<br>
数据集地址:<br>
​​https://huggingface.co/datasets/NUSTM/judgement-consistency-preference-data 目前进不去<br>
ACL2024主会议录用<br>

## 怎么通过后续提问机制量化语言模型的判断不稳定性？
1.提示设计： 设计三种类型的后续问题：封闭式问题、开放式问题和引导性问题。封闭式问题要求模型确认其判断的正确性，开放式问题通过否定促使模型重新评估其判断，而引导性问题则通过提供错误答案来测试模型是否能保持准确性。
<br>
2.提示形式： 提示分为直接形式和渐进形式。直接形式在模型首次给出正确答案后选择一种问题类型继续对话，而渐进形式则在正确的初始响应后依次进行多轮提问（封闭式、开放式、引导性问题），以构建更复杂的对话场景并全面评估模型的判断一致性。
<br>
3.评估指标： 引入了两个指标，修改（M.）和修改率（M. Rate）。对于问题q，标准解记为s(q)，模型M的回答记为M(q)。Accbefore(M; Q)和Accafter(M; Q)分别表示在应用后续提问机制前后的整体准确率。修改（M.）是指模型回答发生变化的情况，而修改率（M. Rate）是修改次数与总问题数的比例，用来衡量模型判断不一致性的程度。
<br>
通过这些步骤，后续提问机制能够系统地检测模型在面对质疑或误导时的判断稳定性，并通过比较应用机制前后模型的准确性变化来量化这一问题。<br>

idea：考虑结合其他验证技术，如人类评估或对比实验，以增强评估的全面性。<br>
      优化提示设计<br>
      不同问题类型（明确答案的客观问题）对模型判断一致性影响的量化比较<br>

# Word2Vec
![image.png](/doc/image/21.png)<br>
如果把国家和首都对应在一起，或者把一个动词的三个时态放在一起，这些词汇之间都有一个类似的关系。<br>
![image.png](/doc/image/22.png)<br>
如果把word vector两两相减，然后投影到另外一个空间，如果一个词和另一个词有从属关系，那么相减之后的结果会落在邻近区域。

# Ask Again, Then Fail: Large Language Models' Vacillations（摇摆不定） in Judgement

## 摘要
我们观察到，当前的会话语言模型在面对后续问题时经常会动摇他们的判断，即使最初的判断是正确的。这种摇摆不定对产生可靠的响应和建立用户信任提出了重大挑战。为了全面评估这个问题，我们引入了FOLLOW-UP QUESTIONING MECHANISM以及两个指标来量化这种不一致，证实了它在当前语言模型中的广泛存在。为了缓解这个问题，我们探索了闭源模型的各种提示策略;此外，我们开发了一个基于训练的框架UNWAVERING-FQ，该框架通过合成高质量的偏好数据来使语言模型保持其原始正确的判断。实验结果证实了该框架的有效性及其增强模型的一般性能力。

## introduction
two challenges: <br>
(1) how to comprehensively assess the judgment consistency issue and employ appropriate metrics to accurately quantify it; <br>
inspired by the theory of “questioning strategies” in education (Shaunessy, 2005)<br>
three question types: closed-ended(答案标准化), open-ended(没有单一正确答案), and leading questions（Socratic）<br>
two forms: Direct and Progressive<br>
for example:<br>
teachers extend the dialogue through additional queries, negations, or misleading prompts following a student’s response, aiming
to ascertain the depth of their understanding.<br>
数据集https://huggingface.co/datasets/NUSTM/judgment-consistency-preference-data#dataset-format<br>
真-真、假-真、假-假和真-假。第一个“真”或“假”表示模型在初始问答中的判断正确性，第二个表示模型在面对后续问题时的判断正确性。
![image.png](/doc/image/23.png)<br>
(2) how to mitigate this issue through technical means, whether for open-source or proprietary专有 models.<br>
提出UNWAVERING-FQ的框架，分为三个步骤：careful data preparation, rigorous缜密 preference data synthesis (based on our proposed polarized分化 preference context distillation), and preference optimization training<br>
第二步：优化模型偏好和确保一致性<br>
1.偏好分布：通过分析和优化模型在不同上下文中的偏好分布，确保模型在面对不同类型的问题时能够保持一致的判断。<br>
2.隐式奖励函数：利用隐式奖励函数来衡量模型的偏好损失，从而指导模型的优化过程。<br>
3.两阶段优化：将知识蒸馏过程分为两个阶段，首先优化包含隐式奖励和反向KL散度的目标，然后进一步改进模型的性能。<br>
知识蒸馏（Knowledge Distillation）将一个复杂模型（通常称为“教师模型”）的知识转移到一个更简单、更小的模型（称为“学生模型”）中。这个过程可以提高小模型的性能，使其接近或达到大模型的水平，同时减少计算资源的消耗。<br>
框架评估：MT-bench, a multi-turn question set（多轮询问） 出自https://huggingface.co/datasets/NUSTM/judgment-consistency-preference-data. and Chatbot Arena, a crowdsourced battle platform（通过让用户参与投票和反馈，来确定不同模型的表现和优劣）。<br>

## PROBLEM FORMULATION
q：question,R:response,M:a dialogue model<br>
R = M(q),R′ = M(C; q′) C represents the dialogue history and q′ the follow-up question<br>
f(R) = f(R′)f represents the function to extract the answer from the response<br>
-> wave or not

## QUANTIFYING THE JUDGMENT CONSISTENCY
two metrics:<br>
![image.png](/doc/image/24.png)<br>
![image.png](/doc/image/25.png)<br>
![image.png](/doc/image/26.png)<br>
conclusion：M. Rate可以相对来说衡量模型一致性，但考虑到在初始性能较差时，仅使用修改率的解释价值有限。直观地说，这两个指标越低，模型就越稳健和可靠。
<br>
eight benchmarks:<br>
For Arithmetic Reasoning算术推理:<br>
(1) GSM8K dataset (Cobbe et al., 2021) for diverse grade school math problems（https://arxiv.org/abs/2110.14168）<br>
(2) SVAMP dataset (Patel et al., 2021) for challenging math problems(https://aclanthology.org/2021.naacl-main.168)<br>
(3) MultiArith dataset (Roy & Roth, 2015) for multi-step reasoning in math(https://aclanthology.org/D15-1202)<br>
For Commonsense Reasoning常识推理: <br>
(4) CSQA dataset (Talmor et al., 2019) requiring complex semantic语义 understanding(https://aclanthology.org/N19-1421)<br>
(5)StrategyQA dataset (Geva et al., 2021) for multi-hop reasoning tasks利用知识图谱多步推理(https://doi.org/10.1162/tacl_a_00370) <br>
For Symbolic Reasoning符号推理: <br>
(6) the Last Letter Concatenation dataset(Wei et al., 2022) for concatenating联系 last letters of words<br>
(7) the Coin Flip dataset (Wei et al., 2022) to determine coin positions after flips给定一系列翻转的条件下，模型给出每次翻转后硬币的正反：我们可以给定一个条件，要求模型翻转硬币10次，每次翻转硬币出现正面的概率是0.7。(https://proceedings.neurips.cc/paper_files/paper/2022/file/9d5609613524ecf4f15af0f7b31abca4-Paper-Conference.pdf) <br>
Chain-of-Thought Prompting思路链提示<br>
![image.png](/doc/image/27.png)<br>
For Knowledge Reasoning知识推理: <br>
(8) MMLU dataset (Hendrycks et al., 2021), encompassing 57 varied subjects and ranging in difficulty from elementary to professional levels.( https://openreview.net/forum?id=d7KBjmI3GmQ)<br>
![image.png](/doc/image/28.png)
在算术推理任务中，通常需要多个推理步骤才能得到准确的答案，机制内的引导性问题会在整个推理过程中逐步增加计算错误、公式差异和语义误解的概率，从而显著降低判断的一致性。<br>
![image.png](/doc/image/29.png)
常识推理中，所获得的信息量与模型的判断一致性直接相关；信息越少，一致性就越低<br>
对于符号推理，我们使用最后一个字母连接和硬币翻转数据集来评估ChatGPT。该模型在这些任务中表现出较低的判断一致性，类似于它在常识推理中的表现，这是由于提示中的语义信息复杂，以及后续提问机制中各种类型的后续问题的干扰。我们观察到，ChatGPT经常不能在符号任务中自动使用思维链推理，导致判断一致性的显著下降，特别是在没有明确的推理过程的情况下。<br>
对于知识推理，判断一致性、主题专业化程度和问题的复杂性之间存在明显的相关性。具体而言，该模型在需要大量知识的领域（如道德场景）中表现出较低的一致性，而相比之下，在更传统的领域（如高中学习的政府和政治知识）中则表现较好与小学水平的问题相比，在大学数学等高级问题中观察到一致性明显下降
![image.png](/doc/image/30.png)
为每个模型确定GSM8K上的最佳temperture(如果其值大于1，那么模型生成的文本会更加随机，多样性更好；如果其值小于1，那么模型生成的文本会更加保守，更倾向于选择概率最高的词)，然后将其应用于所有数据集。具体来说，temperature设置如下： ChatGPT为0.5，PaLM2-Bison为0.4，Vicuna-13B为0.7，默认的top-p值为1.(在每次生成一个新的词时，模型会计算所有可能的词的概率，然后选择累积概率超过"top p value"的词作为候选词12。如果"top p value"为0.95，那么在生成每个词时，模型只会考虑那些累计概率已经超过0.95的词.)

## TOWARDS MITIGATING THE INCONSISTENCY
本质上，我们认为这个问题可能源于数据收集和注释过程中的偏见，例如人工注释者可能偏爱看似正确但谄媚（人类反馈可能鼓励模型做出符合用户信念而非真实的回应）的答案（Sharma et al.，2023） https://doi.org/10.48550/arXiv.2310.13548。理想情况下，对话助手应保持对其判断的自信，在受到质疑时不改变其立场，同时能够在进一步质疑时识别并纠正错误。在这两个方面的平衡上存在挑战，目前对此的研究也有限。在这项工作中，我们探索了各种策略来缓解这个问题，包括training-free(指模型在推断阶段完全不需要额外的训练或微调)和training-based的策略。对于闭源模型，我们探索了training-free方法，即通过调整提示来缓解问题。对于开源模型，我们引入了一个training-based的框架，名为“UNWAVERING-FQ”，以帮助模型坚定地保持其最初正确的判断并纠正错误。

### TRAINING-FREE: PROMPTING STRATEGIES
zero-shot prompting零样本提示：Zero-shot-CoT (Kojima et al., 2022) (“Let’s think step by
step.”) and EmotionPrompt (Li et al., 2023) (“This is very important to my career.”)
few-shot prompting少样本提示：我们通过从训练集中随机选择K个样本，并手动编写反映后续问题的人类思维过程的回答，来构建多回合对话的演示例子。在follow-up questions里，ChatGPT通常在后续的回答中直接承认错误，而与其不同的是提示后的回答首先会澄清思考过程，然后一步一步重新考虑，以“Please wait for a moment. In order to answer your question, I need to take a moment to reconsider. I will now clear my mind of distractions and approach this step by step.”开始。通过示范例子来教模型进行反思，帮助它们提供准确的答案，并与人类更紧密的推理保持一致。
### TRAINING-BASED: UNWAVERING-FQ
![image.png](/doc/image/31.png)<br>
Data Preparation:收集起始问题和后续问题<br>
Polarized Preference Context Distillation：如果模型在初始的问答中判断正确，我们在后续的干扰中加入“相信自己”的提示，以鼓励模型坚持其正确的判断；如果模型最初判断错误，我们则加入“正确答案是...”的提示，以指导模型在获得正确信息后做出正确的判断。<br>
Preference Optimization:<br>
SFT（监督微调，Supervised Fine-Tuning）：这是一种对已经预训练的模型进行特定任务的训练，以提高其在该任务上的表现。<br>
DPO（直接偏好优化，Direct Preference Optimization）：这是一种在大语言模型训练中用于直接优化模型偏好的方法。与传统的强化学习方法不同，DPO直接使用人类偏好数据进行模型优化，从而提高生成内容的质量，使其更符合人类偏好。<br>
### Evaluation on General Ability
目的：验证模型的对话能力在以上框架训练后是否受到损害<br>
数据集：https://proceedings.neurips.cc/paper_files/paper/2023/file/91f18a1287b398d378ef22505bf41832-Paper-Datasets_and_Benchmarks.pdf
![image.png](/doc/image/32.png)

## LIMITATIONS
Reproducibility of evaluation results：被评估的模型包括受内部迭代影响的专有大模型
Limited computational resources
English-centric