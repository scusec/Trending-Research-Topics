# 论文基本信息

## 标题

《Extremely Randomized Trees-Based Scheme for Stealthy Cyber-Attack Detection in Smart Grid Networks》

------



## 作者

[Mario R. Camana Acosta ](https://ieeexplore.ieee.org/author/37087473100)[ ](https://orcid.org/0000-0002-1953-872X); [Saeed Ahmed ](https://ieeexplore.ieee.org/author/37085748434)[ ](https://orcid.org/0000-0002-3624-4096); [Carla E. Garcia ](https://ieeexplore.ieee.org/author/37087471185)[ ](https://orcid.org/0000-0003-4692-253X); [Insoo Koo](https://ieeexplore.ieee.org/author/37275759800)

------



## 出处

[[IEEE Access]](https://ieeexplore.ieee.org/document/8967032)



## 笔者

[殇AD](https://github.com/LCX666)

------



## 主要内容（100-200

作者根据现存智能电网在状态评估期可能会被黑客可以构造假数据以躲避侦测，可以导致整个系统做出错误的决策，进而损害智能电网的安全性，并可能造成生命财产安全事故这一现象，提出了一种基于内核(KPCA)分析降维和超随机树(Extra-Trees)的算法的方法来进行攻击的检测。并且作者通过实验，验证了自己的系统在IEEE 57和118总线基础上比现有的方法具有更优异的表现效果，还能提高智能电网测量中的隐身网络攻击的检测精度。

------



## 创新点（50-150

1、第一个研究噪声干扰标签对SGs SE-MF数据集的影响。

2、提出将KPCA作为非线性降维方法来处理大型电力系统中日益增加的计算复杂性。

3、使用额外树来加速KPCA的计算，比随机森林等可以更好的减小方差。

------



## 缺点分析（50

为了评估更真实的数据，作者往数据中添加了嘈杂标签，但是KPCA在进行降维时又会忽略嘈杂标签，让人怀疑所添加的标签是否真的对更加真实的数据有用，以及系统在真实情况下的表现性能。

------



## 可能性改进（200

如上所述，为了评估更真实地数据，作者添加了嘈杂标签，然后来进行检测，但是其系统的部分算法对该标签并不起作用。因此，或许可以通过调整训练集，往其中人为添加可以构造的假数据，然后在恶意样本中进行检测。也可以在原来的基础上，通过实地采集样本数据，再进行筛选和甄别，再往其中加入恶意数据，这样的方法或许更能体现系统方法的真实性。同样的方法也可以用来扩充正反两面的训练集，以提高自己训练样本集的合理性，进而提升系统的鲁棒性。
