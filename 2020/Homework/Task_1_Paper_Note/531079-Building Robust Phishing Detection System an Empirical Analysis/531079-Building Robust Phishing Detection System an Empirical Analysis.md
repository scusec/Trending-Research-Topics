# Building Robust Phishing Detection System: an Empirical Analysis


## 笔记作者
Sakura

## 基本信息

* 标题
  
  Building Robust Phishing Detection System: an Empirical Analysis
  
* 作者

  Jehyun Lee∗, Pingxiao Ye†, Ruofan Liu∗, Dinil Mon Divakaran†, Mun Choon Chan∗

* 刊物出处：

  Network and Distribute Systems Security(NDSS), Workshop on Measurements, Attacks, and Defenses for the Web, February 23, 2020, San Diego, California

* 链接：
  
  https://www.ndss-symposium.org/wp-content/uploads/2020/02/23007.pdf

## 论文简要

  机器学习算法通过良性和钓鱼网站URL及内容训练出的二分类模型广泛应用于检测网络钓鱼攻击，但是攻击者可通过模仿良性网页的特征值来进行绕过。本文基于此提出了一种基于投票的检测系统并采用了模型，每个模型都由从整个特征集中随机选择特征子集并插入噪声进行训练。最后基于真实数据集和多种绕过策略证明了该检测系统相较传统机器学习模型具有准确度接近且鲁棒性强的优点


## Process diagram

![JWaaY4.png](https://s1.ax1x.com/2020/04/27/JWaaY4.png)

首先对训练集和特征集进行特征提取，然后进行特征选择，在特征集中的一部分子集插入一些可控噪音，在此基础上训练出不同特征空间的多个分类器，最后通过投票法对生成的多个分类器的结果进行决策，得出最终的分类结果。

## 主要内容

1. Steps
  * (1) changing the feature ranking of a model using noise insertion. 使用噪声插入的方法来改变模型特征值重要性的排序
  * (2) Building multiple models having diverse feature rankings. 从每个特征子集中随机选择特征个数，并将随机噪声插入到相应的值中，从而创建具有不同特征排序的多个模型
  * (3) building a robust phishing page detection system with the multiple models.  本文考虑了将以下两种方法结合起来构建一个鲁棒性强的钓鱼页面检测系统
      * (a) 从n个模型中随机选择一个对每次输入的URL进行分类，并将该模型的输出作为分类结果。这种方法虽然简单，但不允许对手猜测哪个模型用于分类，从而削弱了绕过攻击
      * (b) 使用一个投票系统，它根据每个模型的输出来决定;输出最多的那个类别(钓鱼网页或正常网页)即为最终的预测值
      * (c) 称第一个系统为R，称第二个系统为V
2. Evaluation
  * 数据集
     * 良性URL：从Alexa top websites 前30万个域名中收集了110090个HTML页面样本
     * 钓鱼URL：2019年5月30日至7月10日期间的PhishTank数据库的daily feed。共得到了32,159个钓鱼页面
     * 90%作为训练集，10%作为测试集
  * 绕过策略：Random feature attack, Evasion assuming knowledge of modelgeneration algorithm, Evasion assuming knowledge of the algorithm and partial knowledge of operation
  * 评估结果
     * 经过噪音训练后的模型在面对绕过攻击时比原始模型鲁棒性更强，而面对无绕过攻击的钓鱼网站时两者检测性能差异不大。
     * 当面对无绕过攻击的钓鱼网站时，原生模型和R、V系统性能差异不大，而当攻击者使用不同的绕过策略后，性能最好的是投票系统V，其鲁棒性最强。


 ![JfEaa8.png](https://s1.ax1x.com/2020/04/27/JfEaa8.png)

​    


## 创新点

* 使用了多种模型对输入的URL进行分类，避免了对手猜测哪个模型用于分类，从而削弱了绕过攻击
* 将投票法与多种模型相结合，提高了准确性
* 插入噪声降低了分类器的特征权重
* 考虑了多种绕过策略

## 不足之处

* 分类器只考虑了随机森林，虽然后续本文初步研究了SVM在钓鱼检测中的性能，但是由于本文所采取的噪声插入方法并没有提高SVM的鲁棒性，故未做深入研究
* 多模型的方法成本较高，实际应用效果可能会下降
* 本文对于绕过攻击的策略是自己假设的，未考虑是否适用实际生产环境中

