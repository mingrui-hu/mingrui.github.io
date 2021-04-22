---
layout: post
title:  "GAN Day1 Introduction"
categories: gan
---
# Day1 Introduction

## 1. GAN 应用：

- 数据生成
- 图片翻译
- 超分辨率
- 动作迁移

## 2. 发展

from 2014 onwards, 2018 exponential development

**6个方面**

- 网络结构
- 条件生成网络
- 图像翻译
- 归一化和限制
- 损失函数
- 评价指标

论文timelines



### 3. 原理

- **Loss Function**： 

- $min_G max_D  = E_{x~P_r}[log(D(x))] + E_{z~P_z}[log(1-D(G(z)))]$ 

- Min, max 指的是输入为**真实值**的概率

  $ P_r$(or $P_{data}$): 实际数据分布

  $P_z$：随机噪声分布

- 迭代/训练过程：

  - 依次: 固定Discriminator -> 固定generator， 训练discriminator-> 再固定discriminator, 训练generator。。。。
  - 

- 输入输出
  
  - 目标： 输入一个噪声， 生成一个图片
- Compare： AE
  - 最大区别(really?)：loss function
    - AE: point-wise loss -> 模糊但稳定
    - GAN: distribution match -> 清晰但不稳定

### 4. 一点点理论

- 生成器拟合真实分布 $U(0, 1) -> f_{gen} -> P_r$
- 判别器分布
- 判别器训练
  - generator 权重固定 :
  -  $ G(z) = \tilde{x}$ -> 二分类损失函数 (BCE)
  - 标签设为0

- 生成器训练
  - loss func 第一项无关
  - 生成器的标签 -> not real image, set to **1** 

## DCGAN

1. ? 多个线性层直接连接，没用啊？
2. unsupervised representation learning with **deep convolutional generative adversarial networks**
3. Components:
   1. Gen: Upsampling: ConvTranspose
   2. BatchNorm
   3. Gen: Relu
   4. Disc: LeakyRelu
4. Codes:
   1. Note: 2 optimizers
5. Question: multiclass?
6. 

