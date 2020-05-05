# Distributed Quickest Detection of Cyber-Attacks in Smart Grid

### 论文笔记作者：魏来 2017141451031

## 论文基本信息

#### Authors：Mehmet Necip Kurt, Yasin Yılmaz

#### Link：🔗https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8278264

#### From：🔗https://dblp.uni-trier.de/db/journals/tifs/tifs13.html[*IEEE Transactions on Information Forensics and Security*, vol. 13(CCF推荐会议,TIFS)]



## 论文主要内容:

文章针对智能电网中随机化和结构化的虚假数据注入攻击（FDI）以及拒绝服务攻击（DoS）两种攻击方式的检测技术展开了研究。作者将电网系统建模为离散时间线性动态系统，利用卡曼滤波器进行状态估计，采用了广义积累和（CUSUM）的算法，能够对分布式系统和集中式系统遭受的网络攻击进行快速、在线的检测，且这种检测技术在时变状态、攻击等方面具有较好的鲁棒性。根据实验结果，文章提出的检测器对于FDI和DoS攻击具有可靠且迅速的响应效果。此外作者还提出了一种新的基于事件的滞后交叉采样方案（LCSH），与传统的均匀时间采样方案相比，具有明显的优势。

![](https://pic.downk.cc/item/5e968673c2a9a83be56dcb6e.png)

## 论文创新点：

- 针对智能电网中的FDI和DoS攻击，提出了一种新颖的、低复杂度的实时检测方案，可以应用于分布式或集中式架构的智能电网。文章提出的方案对未知的和随时间变化的攻击强度、受到攻击的电表集（set of attacked meters）以及系统状态具有较好的鲁棒性。

- 对攻击变量进行在线评估，对于减轻攻击以及系统恢复至关重要。此外还导出了攻击幅度和攻击电表集（set of attacked meters）的简单闭式最大似然估计（MLE）表达式。

- 文章提出的FDI检测机制可对论文 “False data injection attacks in electricity markets,”中描述的隐蔽FDI攻击进行检测。

- 提出了一种新的基于信息滤波器的分布式动态状态估计器。

- 此外，在分布式环境下，提出了一种新的事件触发采样方案——LCSH，用于本地统计信息的采样和传输，与传统的均匀时间采样（US）方案相比，它显示出显著的优势。

  ![](https://pic.downk.cc/item/5e96a46bc2a9a83be583da8a.png)

## 论文的缺点：

- 论文实验采用的为IEEE-14 bus power system，分为4个子区域，仅有23个电表，14条总线，规模较为有限。考虑到实际中智能电网的规模往往很大，因此文章提出的方法在实验条件下的结果可能与实际情况存在偏差。

  <img src="https://pic.downk.cc/item/5e96a3a6c2a9a83be5834e75.png" style="zoom:80%;" />

- 论文实验中，假设子控中心和总控中心之间的信息传输是即使通讯，即不存在延时，而在现实中这种条件是不可能达到的，因此实验条件过于理想化。

## 解决该问题可能采用的其他替代方案或对本篇论文缺点的改进方法：

- 本篇论文在实验中可以采用规模更大的电力系统进行实验。

- 论文（🔗https://ieeexplore.ieee.org/document/6982207）中提出的机遇广义似然比（GLR）的新型CUSUM类算法可以被用于集中式和分布式网络中的FDI检测，对于各种攻击策略以及电力系统中的负载情况具有鲁棒性，且计算效率高，计算复杂度随着电表的数量呈线性比例关系。在平均延迟检测以及对各种攻击策略鲁棒性方面，大大优于现有的检测技术。

- 论文（🔗https://www.researchgate.net/publication/228373879_Detecting_False_Data_Injection_Attacks_on_DC_State_Estimation）提出通过策略性选择一组传感器的测量值进行保护并结合独立验证或测量策略性选择的一组状态变量的值的方法来对FDI进行检测。

  



