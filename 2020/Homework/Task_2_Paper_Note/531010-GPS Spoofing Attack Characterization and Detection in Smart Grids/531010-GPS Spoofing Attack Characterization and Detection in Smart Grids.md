# GPS Spoofing Attack Characterization and Detection in Smart Grids

> 作者 : Parth Pradhan, Kyatsandra Nagananda, Parv Venkitasubramaniam, Shalinee Kishore and Rick S. Blum

> 机构 : Department of Electrical and Computer Engineering Lehigh University, Bethlehem, PA 18015

> 出处 : 2016 IEEE Conference on Communications and Network Security (CNS): International Workshop on Cyber-Physical Systems Security (CPS-Sec)


## 摘要
GPS攻击主要是由于一些PMU上有GPS接收器，GPS欺骗攻击可以通过伪造GPS信号，进而影响时间戳的生成，使得PMU计算数据时产生错误。本文主要阐述了GPS进行定时同步攻击(TSA)的一些特征以及提出基于最大似然估计的方法去检测TSA攻击。最终效果如下，准确率有较大提示，虚警率也保持在较低水平。
![YF8Dsg.png](https://s1.ax1x.com/2020/05/05/YF8Dsg.png)

## 优点
1. 整个论文的论述比较严谨，首先对电力系统进行了类似动力学方面的建模，在这一基础上抽象出TSA攻击的特征矩阵，完成了攻击场景建模。接着使用最大似然估计的数学方法去实现TSA攻击检测，整个论文的结构很清晰，数学论述多。
2. 提出了一种基于最大似然估计的检测方法。


## 不足
1. 数据问题

实验中由于智能电网实验困难(数据采集是智能电网的普遍难题)，采用的是蒙特卡洛方法模拟数据，进行实验。

2. TSA攻击规模

论文假设TSA攻击发生在单个PMU上，但事实上可能存在多个PMU同时遭受TSA攻击的可能。

## 可能的解决方案
1. 针对不足1，我觉得依旧是一个比较困难的问题，只有等实际有数据后能够进行实验。现阶段只能尝试其他随机数据生成算法，因为现实中的TSA攻击可能并不符合特殊分布。
2. 针对不足2给多个PMU指定一个参数p，p为TSA发生的概率，用统计方法去模拟现实中多个PMU遭受攻击的情况，可能可以获得近似的模型。p的设定可以考虑用机器学习的方法优化，只是数据来源依旧是大问题。