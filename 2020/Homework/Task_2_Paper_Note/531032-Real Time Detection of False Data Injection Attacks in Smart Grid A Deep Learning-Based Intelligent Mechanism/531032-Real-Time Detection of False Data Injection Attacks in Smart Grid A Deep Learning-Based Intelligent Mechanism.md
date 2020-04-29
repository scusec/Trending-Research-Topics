-   笔记作者：Rershall
-   原文作者：[Youbiao He ](https://ieeexplore.ieee.org/author/37085906715); [Gihan J. Mendis ](https://ieeexplore.ieee.org/author/37085895544); [Jin Wei](https://ieeexplore.ieee.org/author/38490656200)
-   原文题目：Real-Time Detection of False Data Injection Attacks in Smart Grid: A Deep Learning-Based Intelligent Mechanism
-   原文来源：[IEEE Transactions on Smart Grid](https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=5165411) ( Volume: 8 , [Issue: 5](https://ieeexplore.ieee.org/xpl/tocresult.jsp?isnumber=8013887) , Sept. 2017 )
-   原文链接：https://ieeexplore.ieee.org/abstract/document/7926429

### 主要内容

​		本文利用深度学习技术从而根据历史测量数据识别FDI (False Data Injection) 攻击的行为特征，并能够实时检测FDI攻击。这种检测方法对于攻击场景的假设要求并没有那么严格，且能保证非常高的检测精确度。本文通过IEEE 118总线测试系统的仿真，验证了该检测策略的有效性。本文还使用IEEE 300总线测试系统，评估了提出的检测机制的可扩展性。

### 创新点

- 提出一种新型深度置信网络（CDBN）对大规模历史数据进行高效训练，通过仅对模型网络中的第一个隐藏层进行CGBRBM技术，而对于其他隐藏层均使用常规的RBM技术，从而减少训练时间和复杂度。
- 设计出一种优化模型来描述偷取电力的FDI攻击，假设攻击者使用这种攻击方式，然后用本文提出的CDBN模型去检测。

### 不足

- 训练数据是历史数据，可能对于新型攻击方式检测性能较差，整体鲁棒性差。
- 整体假设条件过多，可能不适用于实际生产环境中
- 检测FDI攻击手段多样性的力度不足，只检测了文中提到的一种电力偷窃攻击。
- 模型对于不同结构的电网系统的实验种类过少，文中只提到了两种。

### 改进方法

1. 针对于文章中出现的参与实验的电网系统种类较少和对检测机制扩展性实验出现的样例不足问题，可以采取适当增加实验样例的办法来解决。比如IEEE 69总线系统，IEEE 14总线系统和IEEE 30总线系统等。
2. 针对于训练数据不够新的问题，可以加入主动学习机制，使用实时的数据监控进行数据采集用于更新模型，从而提升整体智能电网假数据注入攻击检测模型的鲁棒性。同样，对于本文中检测FDI攻击方法较少的问题，也可以通过增加多种FDI攻击模型，对本文设计的FDI检测方案进行性能评估。