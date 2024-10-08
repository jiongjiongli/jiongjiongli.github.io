---
layout: post
title: Deep Learning Notes - Chapter 1
---

# Book

[《Deep Learning》](https://github.com/zsdonghao/deep-learning-book)

# Deep Learning Chapter 1: Introduction

<table>
<tr>
	<th class="table-nowrap">Concept</th>
	<th class="overflow-wrap-hack">Description</th>
</tr>
<tr>
	<td class="table-nowrap">Artificial Intelligence (AI)</td>
    <td>
    <div class="table-content">Intelligent software to automate routine labor, understand speech or images, make diagnoses in medicine and support basic scientific research.
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Machine Learning</td>
    <td>
    <div class="table-content">AI systems acquire their own knowledge by extracting patterns from raw data.
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">AI Deep Learning</td>
    <td>
    <div class="table-content">Computers learn from experience and understand the world in terms of a hierarchy of concepts.
    </div>
    </td>
</tr>
</table>

In the early days of AI, the field rapidly tackled and solved problems that are intellectually difficult for human beings but relatively straightforward for computers --- problems that can be described by a list of formal, mathematical rules. 
Reason: Abstract and formal tasks that are among the most difficult mental undertakings for a human being are among the easiest for a computer.

Challenge to AI:  Problems that human solve intuitively, but hard to describe formally. 
Example: Recognizing spoken words or faces in images. 
Key challenge: How to get informal knowledge into a computer.
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

# Summary

<table>
<tr>
	<th class="table-nowrap">Concept</th>
	<th class="table-nowrap">Input</th>
	<th class="overflow-wrap-hack">Output</th>
</tr>
<tr>
	<td class="table-nowrap">Simple machine Learning</td>
    <td class="table-nowrap">AI</td>
    <td>
    <div class="table-content">Intelligent software to automate routine labor, understand speech or images, make diagnoses in medicine and support basic scientific research.
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Machine Learning</td>
    <td class="table-nowrap">Features</td>
    <td>
    <div class="table-content">Output
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Representation Learning</td>
    <td class="table-nowrap">Original Data</td>
    <td>
    <div class="table-content">Features
    </div>
    </td>
</tr>
<tr>
	<td class="table-nowrap">Deep Learning</td>
    <td class="table-nowrap">Original Data</td>
    <td>
    <div class="table-content">Hierarchical Features 
    </div>
    </td>
</tr>
</table>

