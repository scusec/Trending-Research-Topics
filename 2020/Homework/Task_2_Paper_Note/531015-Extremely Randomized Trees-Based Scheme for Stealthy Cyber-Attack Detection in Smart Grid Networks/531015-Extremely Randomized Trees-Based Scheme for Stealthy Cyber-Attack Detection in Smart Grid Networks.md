# Extremely Randomized Trees-Based Scheme for Stealthy Cyber-Attack Detection in Smart Grid Networks

## 论文基本信息

### 标题

Extremely Randomized Trees-Based Scheme for Stealthy Cyber-Attack Detection in Smart Grid Networks基于极端随机树的智能电网攻击检测策略

### 作者

MARIO R. CAMANA, SAEED AHMED, CARLA E. GARCIA , AND INSOO KOO

### 刊物出处与连接

M. R. Camana Acosta, S. Ahmed, C. E. Garcia and I. Koo, "Extremely Randomized Trees-Based Scheme for Stealthy Cyber-Attack Detection in Smart Grid Networks," in IEEE Access, vol. 8, pp. 19921-19933, 2020.  
<https://ieeexplore.ieee.org/abstract/document/8967032>

## 论文主要内容总结

### 论文摘要

针对问题：攻击者可以在智能电网中构造攻击向量，将偏置值注入到传感器采集的测量数据中，这种SCA-隐形网络攻击不被BDD-坏数据检测器的设备识别。  
研究了智能电网中对用于估计状态变量的测量值，即状态估计-测量特性（SE-MF）的SCA攻击以及BDD如何无法在常规电力系统中检测到，提出了基于KPAC和极端随机化树算法的网络攻击检测的新方法。  
并使用了IEEE 57总线和118总线的标准系统对该方法进行了性能评估，与多个已有的机器学习检测方法对比显示其精度提高的同时，具有较好的性能。  
关键词：KPCA 机器学习 extra-trees  

## 论文主要创新点

1.使用KPCA方法来处理量纲问题  
KPCA作为一种非线性降维的推广方法，不用删除任何的特征进行降维，降低了PCC-电源控制中心的计算成本，处理电力系统中不断增加的计算复杂性，同时保留了大部分原始信息。
  
2.使用极端随机化extra-trees算法进行SCA攻击检测  
将KPCA的投影特征作为输入，对正样本与被攻击样本进行分类。在对连续变量特征选取最优分裂值时，不会计算所有分裂值的效果，来选择分裂特征，而是对每一个特征，在它的特征取值范围内，随机生成一个split value，再计算看选取哪一个特征来进行分裂。extra-trees是一种集成方法，计算效率高且精度高，对比随机森林和AdaBoost，极端的随机化更能减少方差和偏差。（方差是由于模型对训练集中的小波动过于敏感，高方差会导致过拟合）在特征子集的选择和割点上采用显示随机化，从而减少了方差。使用了完整的原始训练数据集来学习每一个decision tree，来最小化偏差，提升了泛化能力。
  
3.提出了集中式和分布式的两种方案  
集中式的方案：所有仪表的测量都在PCC和攻击检测的程序中进行处理，该结构的发电、输电、配电系统通过变电站和传输线相互连接，与操作中心的通信通过广域网、局域网、场域网组成，收集的测量数据通过SCADA系统中的远程终端单元RTU传输到PCC-电源控制中心，然后使用本文的检测方法进行攻击检测识别。
分布式的方案：本地任务中心在子域收集处理仪表测量数据，同时与邻近的本地控制中心和全球中心保持通讯联系。假定本地中心和全局中心之间的传输局部统计和控制信号是瞬时的，则采用本文检测算法，将每个i中心检测到的SCA攻击在一个可能的状态估计，与邻近中心共享数据，然后各个本地中心的检测结果传输到全球中心。
  
4.首次进行了研究噪声标签对智能电网中状态估计-测量特性（SE-MF）数据集的影响  
研究有噪声标签的分类，其中训练数据集中真实标签的百分比是独立的，进行随机加噪损坏。测试集也存在无加噪的不可见数据。

## 论文缺点

1.集中式的方式难以实现广域智能电网使每个子域的无线通信基础设施与全球中心通信  
2.攻击数据的生成模型是假设攻击者知道了电网所有的拓扑结构信息生成的，该数据集虽然有随机和加噪处理，但是否会造成模型的泛化能力不好，只能检测此类的特定数据规律攻击？

## 解决该问题的替代方案/改进缺点方法

### 相关方案

由于该论文发表时间较新，从实验的AUC结构和鲁棒性可以替代此方案或更优的实验数据暂时没有，所以按时间线总结类似工作的不断改进过程  
1.基于概率分布来预测异常操作行为的高斯过程回归的SCA检测策略
Z. Fadlullah, M. Fouda, N. Kato, X. Shen, and Y. Nozaki, ‘‘An early warning system against malicious activities for smart grid communications,’’ IEEE Netw., vol. 25, no. 5, pp. 50–55, Sep. 2011.

2.基于PCA来检测假数据注入攻击
J. Hao, R. J. Piechocki, D. Kaleshi, W. H. Chin, and Z. Fan, ‘‘Sparse malicious false data injection attacks and defense mechanisms in smart grids,’’ IEEE Trans. Ind. Informat., vol. 11, no. 5, pp. 1–12, Oct. 2015.

3.基于PCA数据降维对SVM进行超标记训练检测假数据注入攻击
M. Esmalifalak, L. Liu, N. Nguyen, R. Zheng, and Z. Han, ‘‘Detecting stealthy false data injection using machine learning in smart grid,’’ IEEE Syst. J., vol. 11, no. 3, pp. 1644–1652, Sep. 2017.

4.基于遗传算法和SVM高斯核函数算法检测方法
M. Esmalifalak, L. Liu, N. Nguyen, R. Zheng, and Z. Han, ‘‘Detecting stealthy false data injection using machine learning in smart grid,’’ IEEE Syst. J., vol. 11, no. 3, pp. 1644–1652, Sep. 2017.
  
5.基于PCA和无监督iforest算法检测数据完整性攻击
S. Ahmed, Y. Lee, H. Seung-Ho, and I. Koo, ‘‘Unsupervised machine learning-based detection of covert data integrity assault in smart grid networks utilizing isolation forest,’’ IEEE Trans. Inf. Forensics Security, vol. 14, no. 10, pp. 2765–2777, Mar. 2019.

### 改进方法

1.未来的5G技术可以给本论文集中式的检测方式提供更好的效果  
2.扩展攻击向量的生成思路与方法和扩大数据集样本多样性  
