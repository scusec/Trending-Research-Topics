---
typora-copy-images-to: ./
---

- 笔记作者：blz 2017141531031
- 原文题目：Building Robust Phishing Detection System: an Empirical Analysis

- 原文作者：

  Jehyun Lee∗, Pingxiao Ye†, Ruofan Liu∗, Dinil Mon Divakaran†, Mun Choon Chan∗ 

  ∗National University of Singapore 

- 原文来源出处：NDSS 2020会议

- 原文链接：https://www.ndss-symposium.org/wp-content/uploads/2020/02/23007.pdf

针对对手试图通过模仿良性网页（特征值）来逃避基于ML的钓鱼网页分类器，提出了一种健壮的基于投票的多模型钓鱼网页检测系统。通过在整个功能集中随机选择的特征子集中插入（受控）噪声来训练多个不同模型，投票系统根据每个模型的输出进行决策。使用真实的数据集进行了全面的实验，采用多种规避策略，评估表明，提出的系统在没有对抗性攻击的情况下性能接近于原始模型，且比模型更能抵抗逃避攻击。

### 1、论文思路

<img src="https://s1.ax1x.com/2020/04/29/J7JJU0.png" alt="J7JJU0.png" style="zoom: 50%;" />

### 2、研究内容

总结其他论文常用的检测钓鱼的特征，作为自己训练模型的特征

[<img src="https://s1.ax1x.com/2020/04/29/J7JsV1.png" alt="J7JsV1.png" style="zoom: 80%;" />](https://imgchr.com/i/J7JsV1)

分类器性能展示，随机森林效果最好，所以后面的实验研究的分类器均为随机森林

[![J7te1S.png](https://s1.ax1x.com/2020/04/29/J7te1S.png)](https://imgchr.com/i/J7te1S)

[![J7YGsH.png](https://s1.ax1x.com/2020/04/29/J7YGsH.png)](https://imgchr.com/i/J7YGsH)图1



图 1 使用多个分类器构建健壮的检测系统的建模过程

1. 使用噪声插入来更改模型的特征等级

2. 创建具有不同特征等级的多个模型

3. 使用多个模型构建健壮的网络钓鱼页面检测系统。

   随机选择特征的结果展示

   [![J7Ygwn.md.png](https://s1.ax1x.com/2020/04/29/J7Ygwn.md.png)](https://imgchr.com/i/J7Ygwn)

   根据特征重要排行表，选择前十个中至少五个，结果如下，效果明显更好

   [![J7YFRU.png](https://s1.ax1x.com/2020/04/29/J7YFRU.png)](https://imgchr.com/i/J7YFRU)

   最后，对随机选择的多模型系统与基于投票的多模型系统进行对比，基于投票的系统性能更好

   [![J7YqT1.png](https://s1.ax1x.com/2020/04/29/J7YqT1.png)](https://imgchr.com/i/J7YqT1)

   

### 3、创新点

本文的主要创新点在于：

1. 基于单个特征向量和给定的固定训练集生成多个随机模型，并将这些生成的模型用于构建健壮的多分类器检测系统。
2. 将基于投票的分类器引入其中，通过实验证明投票可以提高的单纯多模型分类器的准确率

### 4、论文评价

本文提出的方法基于投票策略的多模型钓鱼检测系统思路较为清晰，有不错的参考价值，且作者思路清晰，图文合理，适合阅读；但作为一篇会议论文，似乎较为单薄，关键技术几乎没有设计算法创新或者提出新技术等，且在威胁模型中提出白盒和黑盒模型两种，但所解决的问题更多是建立在白盒攻击上；

除此之外，本文所有实验全部集中于随机森林这一种分类器，不太具有代表性，可以在广泛使用的SVM或者其他分类算法上进行尝试，验证方法的有效性。



