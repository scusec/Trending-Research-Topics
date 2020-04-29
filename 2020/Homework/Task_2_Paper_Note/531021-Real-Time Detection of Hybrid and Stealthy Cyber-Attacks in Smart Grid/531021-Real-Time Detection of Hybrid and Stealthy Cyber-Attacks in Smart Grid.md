### 基本信息

- 标题：Real-Time Detection of Hybrid and Stealthy Cyber-Attacks in Smart Grid

- 作者：[Mehmet Necip Kurt ](https://ieeexplore.ieee.org/author/37085771598)[ ](https://orcid.org/0000-0001-5827-2533); [Yasin Yılmaz ](https://ieeexplore.ieee.org/author/38530048400)[ ](https://orcid.org/0000-0003-2014-3060); [Xiaodong Wang](https://ieeexplore.ieee.org/author/37086427000)
- 刊物出处：M. N. Kurt, Y. Yılmaz and X. Wang, "Real-Time Detection of Hybrid and Stealthy Cyber-Attacks in Smart Grid," in *IEEE Transactions on Information Forensics and Security*, vol. 14, no. 2, pp. 498-513, Feb. 2019.
- 链接：https://ieeexplore.ieee.org/document/8409487
- 作业提交地址：https://github.com/cjrcjr/Trending-Research-Topics/tree/patch-1/2020/Homework/Task_2_Paper_Note



### 主要内容总结

- 针对什么问题
  - 本文研究了智能电网中混合FDI/干扰攻击的实时检测
- 做了什么工作
  - 提出能够及时发现潜在的联合和隐蔽设计的FDI和干扰攻击的机制。该机制使得检测和状态估计方案对未知攻击和时变攻击变量都具有鲁棒性。
- 实现了什么目标
  - 针对（可能）FDI和干扰攻击的组合，提出了一种新的低复杂性在线检测和估计算法。建议的算法对未知和时间变化的攻击类型、幅度和攻击仪表集是可靠的。此外，还介绍了恢复状态估计值和封闭形式的联机 MLE 攻击变量估计值。
  - 介绍了和分析对基于CUSUM的探测器的隐秘攻击，尤其是对所提议的算法的攻击。
  - 提出了几种针对被视为隐蔽的攻击的对策。



### 创新点（50-150字）

- 提出了一种基于 CUSUM 的在线攻击检测和估计算法

- 还以封闭形式提供了攻击参数的在线估计值，并在发生网络攻击时恢复了状态估计值

- 提出了广义的Shewhart测试和滑动窗口气方测试，对抗非持久性和持续性隐身攻击

  

### 论文的缺点

- 提出的混合攻击模型没有涵盖网络拓扑攻击



### 对本篇论文缺点的改进方法

- 作为未来的工作，可以考虑通用状态估计机制（generalized state estimation mechanism），使得系统状态和网络拓扑可用根据power flow / injection measurements、有关网络交换机和线路断路器状态的测量进行估算
- 可以制定针对高级拓扑攻击的对策，在高级拓扑攻击中，攻击者同时执行混合FDI /干扰和网络拓扑攻击。



