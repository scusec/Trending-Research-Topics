#1.论文信息
* 笔记作者:龙泷
* 原文作者：Mohammadhafez Bazrafshan，Hao Zhu，Amin Khodaei，Nikolaos Gatsis 
* 原文题目：Online Demand Response of Voltage-Dependent Loads for Corrective Grid De-Congestion
* 原文来源：2019 IEEE International Conference on Communications, Control, and Computing Technologies for Smart Grids (SmartGridComm)
* 链接：https://ieeexplore.ieee.org/document/8909695/
#2.研究内容
在突发事件发生或电网过载期间，需要对电网解堵采取纠正措施。由智能电网的通信能力支持的一个方式就是需求响应（DR）。在本文中，作者利用DR作为纠正工具来实现网格解拥塞。基于DR，作者开发了一种在线电压稳定增强DR算法。
#3.创新点
本文的主要创新点如下：

* 新的基于DR的公式可以轻松处理任何类型的电压相关负载。
* 考虑DR操作的成本。
* DR操作用于电网解拥塞。
* 提供了近似梯度计算，使得算法高度简化，便于分布式实现。
#3.论文缺点
* 没有进行相关的研究说明
* 在算法中存在非线性问题无法正确的表示出来（非凸问题）
* 采用梯度下降算法来解决问题有其局限性
#4.改进办法
* 针对第一个问题，希望研究者在研究前将这方面的研究梳理一下
* 针对第二个优化问题，算法本身也许可以再次优化（这方面我也不是很了解）
* 针对第三个问题，梯度下降不能保证收敛到局部最优解，而现在解决非凸问题有很多办法，如可以优化梯度下降算法（小批量梯度下降），或者可以尝试迭代法来解决（不一定是更优，但有尝试的空间）。
* 还有一个我疑问的点是应用DR是否真的可以优化电网过载问题（文中没有过多提及，只是列出了算法）

