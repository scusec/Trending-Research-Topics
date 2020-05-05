
-   原文作者：Mingjian Cui, Senior Member, IEEE, Jianhui Wang, Senior Member, IEEE, and Meng Yue, Member, IEEE
-   原文题目：Machine Learning-Based Anomaly Detection for Load Forecasting Under Cyberattacks
-   原文来源：IEEE Transactions on Smart Grid. 2019 Jan 3;10(5):5724-34
-   原文链接：https://ieeexplore.ieee.org/document/8600351

### 主要内容

准确的负荷预测可以为电力系统运营商带来经济效益和可靠性效益。然而，对负荷预测的网络攻击可能会误导运营商做出不合适的电力输送操作决策。为了有效、准确地检测这些网络攻击，本文提出了一种基于机器学习的异常检测(MLAD)方法。将一种广泛使用的符号聚合近似(SAX)方法与已有的MLAD方法进行了比较。对公开负荷数据的仿真结果表明，该方法能够有效地检测网络攻击，具有较高的准确率。同时，基于蒙特卡罗仿真的数千种攻击场景验证了该算法的鲁棒性。

### 创新点

- 利用神经网络提供的负荷预测，利用k-means聚类对基准数据和标度数据进行重构。
- 根据尺度数据的累积分布函数和统计特征，采用朴素贝叶斯分类方法对网络攻击模板进行估计。
- 利用动态规划方法对负荷预测数据进行一次网络攻击的发生和参数计算。

### 不足

- 开发的MLAD方法无法找到特定的网络攻击的派生，例如，损坏的拓扑预测模型，伪造的预测参数方法或攻击性的预处理技术。


### 改进方法

1. 关注最新的网络攻击方法，及时更新模型。
