---
title: Embedding-Watermarks-into-Deep-Neural-Networks
date: 2021-10-08 22:23:09
categories:
- 学习
tags:
- paper
- watermark
---

<div align='center' ><font size='6'>Embedding-Watermarks-into-Deep-Neural-Networks导读与复现</font></div>

**Abstract：** Significant progress has been made with deep neural networks recently. Sharing trained models of deep neural networks has been a very important in the rapid progress of research and development of these systems. At the same time, it is necessary to protect the rights to shared trained models. To this end, we propose to use digital watermarking technology to protect intellectual property and detect intellectual property infringement in the use of trained models. First, we formulate a new problem: embedding watermarks into deep neural networks. We also define requirements, embedding situations, and attack types on watermarking in deep neural networks. Second, we propose a general framework for embedding a watermark in model parameters, using a parameter regularizer. Our approach does not impair the performance of networks into which a watermark is placed because the watermark is embedded while training the host network. Finally, we perform comprehensive experiments to reveal the potential of watermarking deep neural networks as the basis of this new research effort. We show that our framework can embed a watermark during the training of a deep neural network from scratch, and during fine-tuning and distilling, without impairing its performance. The embedded watermark does not disappear even after fine-tuning or parameter pruning; the watermark remains complete even after 65% of parameters are pruned.

**abstract of the abstract:** 

* 将一个水印编入神经网络中很有意义，很有前景（废话）。
* 我们通过用parameter regularizer进行水印的编入，这对网络的性能没有影响（重要）。
* 我们做了实验，实验效果很好。

## 1. introduction

