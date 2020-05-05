### 论文基本信息
原文作者：{ [Keke Gai](https://ieeexplore.ieee.org/author/37085461833); [Yulu Wu](https://ieeexplore.ieee.org/author/37086461431); [Liehuang Zhu](https://ieeexplore.ieee.org/author/37692927900);[Lei Xu](https://ieeexplore.ieee.org/author/38239553400);[Yan Zhang](https://ieeexplore.ieee.org/author/37405814700) }

原文题目：Permissioned Blockchain and Edge Computing Empowered Privacy-Preserving Smart Grid Networks

原文来源： *IEEE Internet of Things Journal* 

文章链接： https://ieeexplore.ieee.org/abstract/document/8664577

笔记作者昵称：Gossipboy

### 主要内容总结
在智能电网带来便利的同时，它也带来了安全和隐私问题。于是此文提出了智能电网网络（PBEM-SGN）的模型许可区块链边缘模型，以解决智能网络中的两个重要问题：隐私保护和能源安全。作者使用了团体签名和秘密通道授权技术，以确保用户的有效性，还构建了最佳的安全意识策略通过在区块链上运行的智能合约。
### 主要创新点
1. 使用区块链保证电网信息不可篡改，可追溯；
2. 加强边缘计算保证隐私安全。
### 缺点
1. 延时问题。
由于区块链本身设计问题，信息不能及时更新，于是导致一定的延时问题，不能在信息流极快的电网中发挥很好的作用。
2. 身份验证问题
边缘节点身份需要有效的验证算法。
### 改进方法
1. 智能电网中能源交易十分快速，但是在这个区域区块链不是很适合，可以考虑采用其它去中心化但是又比较快捷的算法，不一定使用区块链技术。
2. 边缘节点的身份验证问题，作者采用ENIV算法，检查EN签名有效性，再验证设定参数。此算法十分繁琐，可能导致性能降低，可以考虑使用更高效的验证算法。
