---
layout: post
title: Deep Learning Notes - Chapter 1
---

# Preface

最近开始阅读[《Deep Learning》](https://github.com/zsdonghao/deep-learning-book)。这让我有了一个边读书边写笔记的动机：写一个这样的笔记，能够让人容易把握住这本书的脉络，从而读懂这本书的核心内容。
由于终究是英文表达更地道，因此该笔记都是节选自书中的原文。只有在我比较有把握的情况下才会给个别概念加上中文翻译。另外，“个人总结”部分是我自己的总结。各位读者如果有建议或意见，欢迎[联系](mailto:jiongjiongai@outlook.com)指正。谢谢！

# Deep Learning Chapter 1: Introduction

<table>
<tr>
	<th class="table-nowrap">Concept</th>
	<th class="table-nowrap">Chinese</th>
	<th class="overflow-wrap-hack">Description</th>
</tr>
<tr>
	<td class="table-nowrap">Artificial Intelligence (AI)</td>
    <td class="table-nowrap">人工智能</td>
    <td>
    <div class="table-content">Intelligent software to automate routine labor, understand speech or images, make diagnoses in medicine and support basic scientific research.
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Machine Learning</td>
    <td class="table-nowrap">机器学习</td>
    <td>
    <div class="table-content">AI systems acquire their own knowledge by extracting patterns from raw data.
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">AI Deep Learning</td>
    <td class="table-nowrap">AI 深度学习</td>
    <td>
    <div class="table-content">Computers learn from experience and understand the world in terms of a hierarchy of concepts.
    </div>
    </td>
</tr>
</table>

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

# 个人总结

<table>
<tr>
	<th class="table-nowrap">概念</th>
	<th class="table-nowrap">输入</th>
	<th class="overflow-wrap-hack">输出</th>
</tr>
<tr>
	<td class="table-nowrap">Simple machine Learning</td>
    <td class="table-nowrap">人工智能</td>
    <td>
    <div class="table-content">Intelligent software to automate routine labor, understand speech or images, make diagnoses in medicine and support basic scientific research.
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Machine Learning</td>
    <td class="table-nowrap">特征</td>
    <td>
    <div class="table-content">最终结果
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Representation Learning</td>
    <td class="table-nowrap">原始数据</td>
    <td>
    <div class="table-content">特征
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Deep Learning</td>
    <td class="table-nowrap">原始数据</td>
    <td>
    <div class="table-content">多层次特征，就像一棵树，上一层特征是下一层特征的抽象。下一层特征更简单。 
    </div>
    </td>
</tr>
</table>
