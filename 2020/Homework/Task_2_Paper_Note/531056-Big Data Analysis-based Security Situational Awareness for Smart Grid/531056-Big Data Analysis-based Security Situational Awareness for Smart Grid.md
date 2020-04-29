# Big Data Analysis-based Security Situational Awareness for Smart Grid

## *笔记作者：网络空间安全学院 韩鑫华 2017141531056*



> **论文基本信息**
>
> 作者：Jun Wu, Kaoru Ota, Mianxiong Dong, Jianhua Li, Member, IEEE, and Hongkai Wang
>
> 单位：Jun Wu and Jianhua Li are with the School of Eletronic Information and Eletrical Engineering, Shanghai Jiao Tong University, Shanghai 200240, China. E-mail: junwuhn@sjtu.edu.cn, lijh888@sjtu.edu.cn .
> • Mianxiong Dong and Kaoru Ota are with the Department of Physics, Department of Information and Electric Engineering, Muroran Institute of Technology, Muroran 050-8585, Japan. E-mail: {mx.dong, ota}@csse.muroran-it.ac.jp.
> • Hongkai Wang is with the Information and Telecommunication Branch of Zhejiang Electric Power Corporation, State Grid Corporation of China, Hangzhou 310007, China. E-mail: wang_hongkai@zj.sgcc.com.cn.
>
> 出处：IEEE Transactions on Big Data 10 October 2016
>
> 链接：https://ieeexplore.ieee.org/document/7587350



## 项目概述

面对组件日益复杂化的智能电网系统以及以APT攻击为代表的多方位风险要素的增多，本文基于关联分析算法，博弈论和强化学习提出了一个智能电网大数据态势感知模型。通过模糊聚类等技术实现了多风险要素的关联输入，以及通过强化学习算法对各要素的相互影响效果进行量化处理，最终实现电网系统的总体安全态势输出。

## 创新点

1. 可处理半结构化和非结构化数据，也能对非线性要素相关关系进行处理。
2. 在纳什均衡基础上进行拓展，结合强化学习算法计算各要素的反馈，实现动态博弈的多智能体强化学习。

## 详细设计

1. 主要算法与流程图示：
   1. 概念图及其实现原则!![](https://i.postimg.cc/sDjpxrN3/image.png)
   2. 安全态势评估![](https://i.postimg.cc/g2r8yKp5/image.png)
   3. 神经网络模型![](https://i.postimg.cc/yYL0SbMc/image.png)
   4. 检测拓扑架构![](https://i.postimg.cc/5NQvyWcr/image.png)
2. 安全态势要素组成：静态配置信息（环境与设备状态——管理设备、代理设备、网络管理中心等）；动态操作信息（日志等）；网络流信息（SNMP相关报文等）。
3. 具体技术：基于等价关系的模糊聚类算法；基于随机策略的强化学习算法；反馈神经网络。

## 项目缺点及改进建议

1. 本方案缺少联动响应模块，可采用Apriori、Eclat、FP-growth等关联规则算法，分析同时出现次数较多的频繁项集，并将出现次数满足一定阈值的频繁项集作为关联项集，得到网元间的联动响应关系。通过引入上下文管理模块，用于加强已知控制策略的保存和自学习，当网络态势及业务目标等发生变化时，在知识库和策略库的支撑下，可利用基于案例的推理（CBR）方法自适应生成和调整控制策略
2. 由检测拓扑架构可知，本方案将态势感知模块与工作区域和产品区域分离开，可能导致的结果是产生风险时无法及时将安全信息传递给其他区域，所以应该对感知模块的网络进行更细粒度的部署设计，设计相关算法保证最小时间复杂度的消息传递。
3. 本项目采用的模糊聚类算法是基于等价关系，它是研究比较早的一种方法，但是在数据量较大的情况下效果并不好，或许可改进成基于目标函数或基于神经网络的模糊聚类算法。