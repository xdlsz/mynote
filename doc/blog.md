### blog for jailbreak
# LLM Jailbreak Attack versus Defense Techniques - A Comprehensive Study
## 摘要
大型语言模型（LLM）已经越来越成为生成具有潜在社会影响的内容的核心。值得注意的是，这些模型已经展示了生成可能被认为是有害的内容的能力。为了减轻这些风险，研究人员采用了安全培训技术，将模型输出社会价值观保持一致，以遏制恶意内容的产生。然而，“越狱”现象——精心制作的提示会引发模型中的有害反应——仍然是一个重大挑战。研究对现有的关于越狱LLM及其防御技术的研究进行了综合分析。我们细致地研究了9种攻击技术和7种防御技术，它们应用于三种不同的语言模型： Vicuna，LLama，和GPT-3.5涡轮增压器。我们的目的是评估这些攻击和防御技术的有效性。我们的研究结果显示，与通用技术相比，现有的白盒攻击表现不佳，并且在输入中包含特殊标记会显著影响攻击成功的可能性。本研究强调了重点关注LLM的安全方面的必要性。此外，我们通过发布我们的数据集和测试框架，为该领域做出了贡献，旨在促进对LLM安全性的进一步研究。我们相信，这些贡献将有助于探索这一领域内的安全措施。

## Q：这篇论文试图解决什么问题？ 
A: 尽管有各种各样的越狱攻击和防御方法，但仍然缺少关于越狱攻击在防御机制下的表现以及防御机制在越狱攻击下的表现的全面评估。我们的研究旨在回答两个关键的研究问题。RQ1：越狱攻击的有效性。RQ2：越狱防御的有效性。

## Q：如何解决这个问题？概述
![image.png](/doc/images/1.png)

## 攻击模型分类
Generative Techniques
<br>Template Techniques
<br>Training Gaps Techniques

## 防御模型分类
Self-Processing Defenses<br>Additional Helper Defenses<br>Input Permutation Defenses

## 实验设计
### Baseline Selection
RQ1:面向五种Generative Techniques(AutoDAN (Liu et al., 2023a), PAIR (Chao et al.,2023), TAP (Mehrotra et al., 2023), GPTFuzz (Yuet al., 2023),GCG(Zou et al., 2023))
<br>四种Template Techniques (Jailbroken (Wei et al.,2023), 77 Templates from existing study (Liu et al.,2023b), Deep Inception (Li et al., 2023a),Parameters (Huang et al., 2024))
<br>RQ2:面向四种防御策略Bergeron (Pisano et al., 2023) for additional helper methods;
<br>RALLM (Cao et al., 2023) and SmoothLLM (Robey et al., 2023) for input permutation
<br>techniques; and Baseline (Jain et al., 2023) for perplexity analysis.

### Benchmark Construction
利用了Liu等人提出的基准测试框架，为了增强我们的评估的鲁棒性，我们扩展了原始数据集，以包括60个恶意查询，有效地将其规模增加了一倍。（数据集扩展方法严格遵循了以往研究中建立的分类和选择标准，确保了增强的数据集进行综合评估的一致性和相关性）

### Result Labeling
难点:手工审查的不切实际和缺乏恶意反应的标准化评估方法<br>
现有策略：Zou等人利用一组常见的拒绝模式，如“对不起”和“我不能”，来自动识别不符合要求的响应。Yu等人和Huang等人分别专注于增强机器学习模型，特别是RoBERTa和BERT-BASE-CASED的模型。此外，Chao等人还探索了利用GPT-4进行攻击分析的方法。<br>
该文章的新策略：利用手动注释的dataset细化RoBERTa模型

### Evalution
RQ1:ASR（ Attack Success Rate）+efficiency
RQ2:DPR（Defense Passing Rate）+BPR（ Attack Success Rate）+CRQ(Generated Response Quality)

## 实验结果
越狱防御的有效性<br>
![image.png](/doc/images/2.png)<br>
越狱攻击的有效性<br>
![image.png](/doc/images/3.png)

## 对于实验结果的讨论

## 有什么可以进一步探索的点？
### 
