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

# Ask Again, Then Fail: Large Language Models' Vacillations in Judgement
在论文评估机制里写出一个








