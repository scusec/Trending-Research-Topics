### 文章信息

**Distributed Framework for Detecting PMU Data Manipulation Attacks With Deep Autoencoders**

IEEE Transactions on Smart Grid 

DOI: 10.1109/TSG.2018.2859339

Author: A team coming from  Huazhong University of Science and Technology.

Jingyu Wang, Student Member, IEEE
Dongyuan Shi, Member, IEEE
Yinhong Li, Jinfu Chen, Hongfa Ding, Member, IEEE
Xianzhong Duan, Member, IEEE

### 内容总结

针对PDMA--相量测量单元的数据操控攻击，提出了一种基于神经网络实现深度自动编码器的分布式PDMA检测框架。基于正常的系统状态数据，用前置反馈神经网络训练模型，配合分布式的架构和一些辅助性手段，实现了高效准确地检测电力系统中的PDMA攻击的功能，此外还可以有效地识别未知状态参数和坏数据参数造成的假阳性，并具有较好的扩展性。

### 创新点

> 使用前置神经网络衡量当前状态与正常状态的偏移程度，从而判断PDMA存在的可能性。

#### 回顾

在说明创新之处之前，有必要回顾一下现有的检测思路。

###### Keeping Basic Measurements Immune from Attacks

有研究表明，只要保证系统的某个特定的关键检测节点集合不会被攻击或者欺骗，就可以保证系统可以识别PDMA和FDI。很显然这个要求很理想化，特别是现在0day漏洞和新式攻击手段层出不穷使得这个要求基本不可能被满足。

###### Formulation Upgrade of State Estimation

对于当前系统环境参数的检测，最终可以归结为weighted least square regression problem，我的理解是一种矩阵和残差计算的问题，PDMA&FDI的原理是改变输入的参数矩阵，却不改变residual的计算结果，从而达到欺骗系统的目的。那么理论上来说，如果针对性修改计算公示，就可以有效避免这种攻击。但是这种方法要求大量地收集高度层次化的数据，而现实中的power grid往往是集中式分布的。

######  Intrusion Detection Systems for WAMSs

思路与网络入侵检测IDS相似，寻找或者建立判断数据是正常还是受操控的一条准则，主要还是依靠开发者的经验来设计判定准则，具体有whitelists-base、rules-based、behavior-based、statistics-based等研究方向，另外就是ML这条路，甚至使用Deep Learning以追求更深层次的数据分析理解能力。但是这样历来扩展能力稍显不足，对大规模系统表现力不从心，同时准备数据集时labeling的工作不可或缺而且工作量很大，而且攻击数据并不是那么好找且充足。

#### 创新

文章提出的方法规避了以上的许多问题，且具有更好的性能表现。

###### feed-forward neural network used in autoencoder and decoder

对于反馈前置神经网络的数学原理我不是很懂，但可以把它理解为一种特殊的函数。
对于输入的状态参数x(由108 个feature组成)，计算y=encoder(x)，然后借助一个特殊的、类似逆函数的decoder()将x重建，即x'=decoder(y)。如果x是一个正常的状态参数，重建值x'会非常接近真实值x，偏差比较小。如果x是一个被操控的值，那么重建值x‘与真实值的偏差会比较大。这时候使用损失函数cost(x,x')来量化这种偏差程度，并合理设定阈值t就可以量化PDMA出现的可能性。

![](https://imgur.com/j8bnbfg.png)

###### Delayed Alert Algorithm

power grid有一个特点就是采样频率很高，于是乎可能出现在一个短暂时间段内的状态参数发生异常，从而被判定为PDMA。文章提出了一个延迟报警函数，用于避免瞬间的状态异常误报，而是总体地考虑一定长度时间范围内的状态偏移情况，可以有效降低误报率。P(patience)代表了系统对这种误报的容忍程度。每当出现误报，p会减少一定的值，检测到一次正常状态，p增加一个微小的值。当p<=0时，系统的容忍度被消耗完，说明这种异常状态出现了较长的持续，应当判定为PDMA。

![](https://imgur.com/9t8N1lB.png)

###### Architecture of PDMA Detection Framework

Anomaly measurer(autoencoder)可以独立地评价anomaly degree(即偏移程度)，但是为了了解整个系统中总体的PDMA存在情况，还是要把数据集中起来分析一下。
考虑到Alert可能是Bad Data引起的，造成了一定假阳性概率。所以控制中心可以向Bad data detection询问，因为一般只有PDMA 生成的data不会被判断为Bad data，这样一来，Bad Data Detection模块可以使得大多数的假阳性警报被纠正。
同时，为了避免一些没有被预测到的特殊状态也可能被误判为PDMA，那么系统需要周期性地收集这些状态，为anomaly measurer更新参数并重新训练，在这个过程中，阈值t也可以考虑被修正。考虑到measurer在系统所处的位置不同，他们会被训练为不同的单元。

![](https://imgur.com/LZ6JH2S.png)

### 优势

> 主要是相对与现有方法/思路的优势

###### 没有前提条件

不用满足保护特定的measurements集合这种不大可能实现的需求

###### Scalability

与centralized相比，distributed architecture减轻了通信负载，提高了性能，同时具有较号的可扩展能力。

###### 自动确定鉴别标准

不用人为设计判定准则
不用大量的手动labeling的工作

###### 不需要攻击数据

本方法建立的神经网络只依靠正常的数据来训练，不需要manipulated measurement。
此外，对电网的攻击虽然存在但绝对数量还是比较少的，更不用说去获取这些数据来做实验或者训练模型，本方法让使用者不用苦哈哈地去找哪些小概率出现的入侵数据。

###### 量化的警报指标

cost函数的结果是量化的，不是简单Boolean反馈，而是反映PDMA出现的概率，更加准确。

### 可能的缺陷

> 作者貌似丝毫没有提及缺陷，这里是一些主观而个人的猜测......

###### Unforeseen Condition

作者对避免unforeseen condition造成假阳性的手段描述地非常简略，让我不由得怀疑作者有意略过这一部分实则并没有提出有效的方法。因为unforeseen condition和manipulated measurement 对于系统来说是等价的，重建参数值x'和原本的值x的差距都比较大。此外，unforeseen condition也不算是Bad Data，也可以持续较长时间，所以只靠文章设计的系统不大可能辨别。

###### Dynamic Condition

Power Grid的状态是持续而频繁地发生变化的，于是要求检测系统的部分参数也要随之发生变换。虽然作者也有提到会有regularly updating，但同样是非常简略。而且这个更新周期如何设定没有提及，更新周期太长，可能跟不上电网的变化，更新周期太短，又会增加系统的负载。

###### Timing

众所周知，智能电网为了实时地掌握系统中的状态，要求数据采集和反馈要足够快速和灵敏。为此，终端设备与其上的程序都被设计得相对简单，通信协议也不是很复杂。现在这个分布式的、部署有多个Anomaly measurer的系统，而且每个Anomaly measurement上面都是一个神经网络，无疑增加了在节点上的计算和设备复杂度，那么是否还满足智能电网对Timing的严格要求呢？

Training

同样，鉴于系统变化的频率很高，那么用历史数据来训练一个符合当前系统现状的神经网络大概不是很现实。

### 改进方案

###### Unforeseen Condition

我认为如果不改进系统，是不大可能识别unforeseen condition的，要不然可以考虑借助系统之外的方法。

比如引入其他可以有效解决这个问题的研究成果做成一个二次检验模块，算是本系统的一个补充。因为unforeseen condition毕竟是个小概率事件，所以可以直接把这个模块加在控制中心，对系统的性能应该不会有太大的影响。

或者在数据准备阶段增加一个步骤，即开发一个系统，遵守Power Grid的一些规律，专门生成各种极端的环境状态参数，预见尽可能多的condition。

###### Timing

合理地规划Anomaly measurer部署的节点位置，比如尽可能地将它们部署在计算能力高的节点，降低对Timing的影响。考虑到Anomaly measurer会不断地被更新迭代且本身就比较复杂，硬件化加速的可能不高。

