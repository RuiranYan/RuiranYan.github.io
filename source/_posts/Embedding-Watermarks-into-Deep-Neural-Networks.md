---
title: Embedding Watermarks into DNN
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

## introduction

训练模型时间会很长，现在有许多finetuning和trasferlearning的方法，未来模型会跟视频图片等一样会有商业价值。本文第一次尝试将水印加入模型。研究主要有三个contributions.

* 公式化了一个新问题，将水印加入DNN，同时定义了需求，场景和攻击类型
* 我们提出了一个普遍的框架（或者说是一个普遍的方法）通过一个parameter regularizer去加入水印，并且这个水印不影响模型的效果。
* 我们做了些实验。

## problem formulation

一些定义：

task: 加入一个 **T** bit的0/1向量 $b\in \{0,1\}^T$ 到网络模型中。被加入水印的模型叫 **host network** ，之前的模型任务叫做 **original task**。

接下来根据introduction我们定义需求场景和攻击类型。

#### 需求：

将模型水印和视频水印进行类比，面对finetuning和transfer learning的模型修改方式要又不变性。

#### 编入水印的场景：

* 训练时编入（从头训练刚开始就编入）
* finetune时编入（网络已经被pretrain过，只有靠近输出层的参数会改变）
* distill编入(distill framework:通过先训练一个大网络再通过大网络的结果训练小网络实现模型压缩)

前两种场景都可以加入私人的水印，但最后一种需要一个可信任平台加入水印。

### 可能的攻击

* fine-tuning or transfer-learning
* model compression

## proposed framework

用DCNN进行实验

### embedding targets

本文中假设将水印编入一个卷积层中，其中(S, S): filter size , D: depth of input to the layer, L: number of filters。这个卷积层参数就是 $W \in R^{S*S*D*L}$ （这里忽略了bias）。这里filter的顺序不应该影响谁赢embed的结果，所以我们对W在L上取平均得到 $w \in R^{M},M=S*S*D$ 。所以embedding目标是将T-bit的b嵌入到w中。

### embedding regularizer

在原有cost function $E(w)$中加入一个正则项 $E_R(w)$ 并不会影响结果只是在w上加入了一些统计上的偏差，所以我们提出了一种正则项能嵌入水印。

首先要给定b和一个T*M的参数矩阵X。

定义:
$$
E_R = -\sum_{j=1}^T (b_j log(y_j)+(1-b_j)log(1-y_j))
$$
其中：
$$
y = \sigma(\sum_i X_{ji}w_i),\sigma (x)= \frac{1}{1+exp(-x)}
$$
将这个正则项加入Loss就能使y接近b，在验证的时候只需计算 $s(\sum_i X_{ji}w_i)$ 与 $b_j$ 进行对比即可，其中 s= x>=0 ? 1:0;(不想打latex就用c写了....)

这样就能通过正则项嵌入水印了。

### regularizer parameters

讨论了各种X的取值方法，主要又三种: $X^{direct},X^{diff},X^{random}$ 具体细节可以去看文章，但文章做了实验发现最后一种效果最好，最后也只用了最后一种X进行了后续实验，所以只讲解 $X^{random}$，其实就是一个X的每个元素通过(0,1)正太分布的独立取样得到。

## 实验

咕咕咕......

