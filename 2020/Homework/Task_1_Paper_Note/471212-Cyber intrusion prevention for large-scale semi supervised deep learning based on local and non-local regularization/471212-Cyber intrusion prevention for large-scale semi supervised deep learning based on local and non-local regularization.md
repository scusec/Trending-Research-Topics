# Cyber intrusion prevention for large-scale semi supervised deep learning based on local and non-local regularization(论文笔记) 

## 基本信息: 

+ 标题: Cyber intrusion prevention for large-scale semi supervised deep learning based on local and non-local regularization
+ 作者: Guangming Xian
+ 刊物出处: IEEE ACCESS  卷: 8  页: 55526-55539
+ 链接: [原文链接](https://ieeexplore.ieee.org/document/9037285?source=authoralert)

## 主要内容总结:

1. 问题: 当前网络环境的复杂性，传统的保护技术已经不能满足网络安全的要求。  

2. 解决方法: 在当前的入侵检测技术和防火墙技术下，提出了一种基于局部和非局部正则化的大规模半监督深度学习的DDBN网络入侵防御新方法. 相关解释如下: 
    + 入侵检测：网络入侵防御的核心技术。结合了入侵检测技术和防火墙技术的优点。这样不仅可以检测到入侵行为，而且可以采取及时的防护措施。

    + 半监督学习方法DDBN：
    半监督学习方法：能够提取更多的鉴别特征，在网络入侵防御任务中具有显著的优势。通过将有监督学习和非监督学习的特性结合起来，半监督学习提供了两种方法的优点。
    DDBN（Discriminative deep belief network区别性深层信念网络)，使系统具有更强的识别性和性能优势。

3. 具体实现: 
    + 使用CD方法对DDBN进行逐层贪婪的预训练
    + 基于局部和非局部正则化的半监督DDBN
    + DDBN的监督微调

4. 效果:

    + 将深度学习应用于网络入侵防御，检测基于入侵数据的隐式攻击行为，降低网络入侵防御的错误率。

    + 利用局部正则化和非局部正则化指数损失函数的DDBN半监督深度学习在网络入侵防御任务中具有更强的识别性和性能优势。

    + DDBN在标记数据稀疏的情况下，利用大量的未标记数据，可以显著提高其网络入侵防御的学习能力。

    + ROC比较表明，DDBN的网络入侵防御效果优于DBN-RFS、GAN、SVM和Hopfield分类器。对比实验表明，该方法能有效降低入侵检测的误分类率。

## 创新点:

1. 提出了一种基于局部正则化和非局部正则化的半监督深度学习方法。

2. DDBN的监督微调：通过优化目标函数对DDBN进行微调，以提取更有利于分类的有效特征

## 缺点分析与改正:

1. 分析
    + 没有background部分，将DDBN与其他几种模型（Hopfield、SVM、GAN）比较时，缺少对已有方法的介绍，

    + 没有future work部分，缺少对未来工作的计划

2. 缺点改正:
    + Hopfield网络是一种典型的递归网络，这种网络通常只接受二进制输入（0或1）以及双极输入（+1或-1）。它含有一个单层神经元，每个神经元与所有其他神经元连接，形成递归结构。
    + 支持向量机（support vector machines, SVM）是一种二分类模型，它的基本模型是定义在特征空间上的间隔最大的线性分类器，间隔最大使它有别于感知机；SVM还包括核技巧，这使它成为实质上的非线性分类器。
    + GEN 模型通过框架中（至少）两个模块：生成模型（Generative Model）和判别模型（Discriminative Model）的互相博弈学习产生相当好的输出。


