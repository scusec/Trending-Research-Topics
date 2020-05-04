# <论文笔记> False Data Injection Attacks With LimitedSusceptance Information and NewCountermeasures in Smart Grid

## 基本信息

作者：Ruilong Deng, Hao Liang

出处：IEEE TRANSACTIONS ON INDUSTRIAL INFORMATICS, VOL. 15, NO. 3, MARCH 2019

链接：https://ieeexplore.ieee.org/document/8425789/

## 主要内容

问题：传统的SCADA系统使用坏数据检测（BDD）来过滤由于仪表故障或恶意攻击而导致的错误测量。然而精心合成的虚假数据注入（FDI）攻击可以绕过BDD，并在不被检测的情况下将随机错误引入状态估计中。通过修改状态变量，FDI攻击可能会误导系统操作员做出错误的决策，并导致有害的控制命令进入电网。

工作：

1. 证明了对手只有在知道与该总线相关的每条传输线的电纳后，才能发起FDI攻击来修改总线上的状态变量。
2. 基于第一点，提出了一种针对FDI攻击的新对策，方案是使n-1条互连传输线的电纳覆盖对手未知的所有总线。

结果：通过一个4总线电力系统和IEEE 9总线、14总线、30总线、118总线和300总线测试电力系统的实例，说明了在有限电纳信息下FDI攻击的实现和新对策的有效性

## 评价

**创新点**

1. 考虑FDI攻击中攻击者掌握输电线路电纳信息有限的事实，使之更接近于真实世界
2. 提供了一种针对FDI攻击的新对策，该对策可以单独使用，也可以与传统方法结合使用，以减少检测FDI攻击所需的仪表测量/状态变量数量

**缺点**

1. 在交流电模型下仍然存在绕过BDD的可能性。
2. 不能快速的定位到可疑的总线

## 其他方案

在`PAMA: A Proactive Approach to Mitigate FalseData Injection Attacks in Smart Grids`这篇文章中提出了一种主动方法来缓解智能电网中的FDI攻击。

具体来说，将状态估计和FDI检测应用程序转换为分布式应用程序，该分布式应用程序具有从控制中心提供的关键信息转换而来的信息，并使用一个安全的混合Paillier PKE来实现密文的分布式计算。PAMA方案很好地保持了H矩阵和原始测量数据z的保密性，这两个数据对于构造FDI攻击都是至关重要的

利用PAMA方案，可以很好地保护用于构建FDI攻击的关键信息-电网连接和配置以及原始测量数据，使FDI攻击得到有效的缓解