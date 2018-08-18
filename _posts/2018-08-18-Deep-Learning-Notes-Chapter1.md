---
layout: post
title: Deep Learning Notes: Chapter 1 Introduction
---

# 前言

最近开始读[《Deep Learning》](https://github.com/zsdonghao/deep-learning-book)一书。这让我有了一个边读书边写笔记的动机：能够让人很轻松流畅的把握住这本书的脉络，从而读懂这本书的核心内容。
由于终究是英文表达更地道，因此该笔记都是节选自书中的原文。只有在我比较有把握的情况下才会给个别概念加上中文翻译。另外，“个人总结”部分是我自己的总结。各位读者如果有建议或意见，欢迎留言。谢谢！

# Deep Learning Chapter 1 Introduction

<!-- | Concept | Chinese | Description |
| - | - | - |
| Artificial Intelligence (AI) | 人工智能 | Intelligent software to automate routine labor, understand speech or images, make diagnoses in medicine and support basic scientific research. |
| Machine Learning | 机器学习 | AI systems acquire their own knowledge by extracting patterns from raw data. |
| Representation Learning | 表示学习 | Use machine learning to discover not only the mapping from representation to output but also the representation itself. |
| AI Deep Learning | AI 深度学习 | Computers learn from experience and understand the world in terms of a hierarchy of concepts. | -->


In the early days of AI, the field rapidly tackled and solved problems that are intellectually difficult for human beings but relatively straightforward for computers --- problems that can be described by a list of formal (形式化), mathematical rules. 
Reason: Abstract and formal tasks that are among the most difficult mental undertakings for a human being are among the easiest for a computer.

Challenge to AI:  Problems that human solve intuitively, but hard to describe formally. 
Example: Recognizing spoken words or faces in images. 
Key challenge: How to get informal (非形式化) knowledge into a computer.
A solution: Machine learning. 

Challenge to simple machine learning: The performance of simple machine learning algorithms depends heavily on the representation of the data they are given. 
Key challenge: What features should be extracted. Feature (特征): The piece of information included in the representation. 
A solution: Representation learning. 

Goal of representation learning: To separate the factors of variation that explain the observed data. Factors: Sources of influence, can be thought of as concepts or abstractions that help us make sense of the rich variability of the data.

Challenge to representation learning: Disentangle the factors of variation and discard the ones that we do not care about.
A solution: Deep learning. 

Method: Introducing representations that are expressed in terms of other, simpler representations.

Two main ways of measuring the depth of a mode:

1. The depth of the computational graph.
2. the depth of the graph describing how concepts are related to each other. It is used by deep probabilistic models, 

<!-- # 个人总结

| 概念 | 输入 | 输出 |
| - | - | - |
| Simple machine Learning | 特征 | 最终结果 |
| Representation Learning | 原始数据 | 特征 |
| Deep Learning | 原始数据 | 多层次特征，就像一棵树，上一层特征是下一层特征的抽象。下一层特征更简单。 | -->
