《Flow Context and Host Behavior Based Shadowsocks's Traffic Identification》

> 基于流的上下文和主机行为的Shadowsocks流量检测方法

### 基本信息：

###### 文章来源

IEEE SPECIAL SECTION ON SECURITY AND PRIVACY FOR CLOUD AND IOT 2019

https://ieeexplore.ieee.org/abstract/document/8676111

###### 文章作者

曾雪梅 			四川大学计算机学院

陈兴蜀 			四川大学网络空间安全学院

四位硕博士 	四川大学网络空间安全学院

王启旭 			四川大学网络空间安全学院

###### 笔记作者

wenake

wenake@qq.com

### 文章简要

Shadowsocks技术的滥用一定程度助长了网络犯罪，也对VPS服务提供商造成一定的威胁。文章在总结前人检测SS流量的方法基础之上，提出了基于Flow Context和Host behavior的检测方法，建立了一个有12个维度的模型，并配合Big data、Big Data Association等技术和方法。总的来说改进或者弥补了前人工作的不足之处，在实验中达到了93%的正确识别率，并适合大规模网络，有利于维护Network和VPS平台的安全性。

### 文章内容概述

###### Background 

 SS这种匿名通信手段滥用于网络犯罪，威胁网络安全，同时对于SS部署的VPS服务商也有影响。

###### Introduction 

 SS这类匿名通信技术有一些比较特殊的地方，比如Invisible Negotiation Process 和 Data Transparent Transmission，这些特点使得对它的检测不容易进行。当然，这些特点也使得SS具备了一些独特的Features，这些将会用在后面对它的检测上来。最后介绍了Contributions，即更高的识别率和适应大型网络的特质。

###### Related Work

介绍了前人在流量识别方面的进展，借鉴思路，指出不足，并以此作为改进的灵感来源。

以前的工作主要分为Traffic Identification 和 Encrypted&Anonymous Traffic Identification两个方面，主要思路为Feature-based,Statistics-based，在Packet level和Flow level两个层面，部分研究借助了分类算法或者机器学习。新的思路是应用数据关联技术，考虑Correlation between Flows Behavior and Hosts Behavior，即流的行为特征与主机行为特征之间的关联，但是没有考虑Flow之间的关联。

以上研究识别准确率在80%-90%范围内，但是有的模型依赖的feature太多，模型过于复杂，在大规模的网络中表现不够好。而且这些研究针对的流量类型很杂，只有两个专门针对SS，其他的有Tor、Skype、VPN、SSL等等，**不能直接套用**，但是具有很大的**参考和借鉴价值**。

###### Analysis of Problem and SS Traffic Characteristics

> 具体问题具体分析

先介绍SS和它的加密通信机制并分析特征，然后启动头脑风暴开始分析。
当然并非完全自创，还是借鉴了前人的一些思路和最近的研究成果，比如Correlation和DNS leakage。

从Flow Context、Host Flow Behavior和Host DNS Behavior各个角度提出新的检测手段，其中会运用到Correlation和Big Data的技术来实现。这部分算是文章的创新所在，所以具体在**改进与创新**部分详细介绍。

###### Detection Method

数学建模与分析过程，从数学模型出发来证明可行性，实在有难度。
主要有数据处理、特征提取以及分类器。由于应用了Big Data和Correlation技术，所以这部分有详细的数学推导过程。

![image-20200407092040763](images\image-20200407092040763.png)

###### Experiment and Result Analysis

实验数据来自校园网流量，那显然就是敝校的校园网了，还使用了大数据分析平台NTCIBDP来完成数据分析和关联工作。在两家VPS服务商上面分别部署了一个SS server，并优化了方法。除了recal rate比以前的某个研究低一点儿，其他的指标都有所提升，而且还适合大型网络且不依赖于时间特征。

###### Conclusion

总结一下Contribution和进步的地方，表示本研究能更加准确的识别SS，可以维护网络的安全，呼应了Abstract和Introduction阐述的现状。

### 主要内容：改进与创新

先介绍SS和它的通行过程，然后得到特点：

**Invisible Negotiation Process**，由于加密参数在部署SS server时预置，所以没有握手或者说协商加密参数的阶段。

**Data Transparent Transmission**，没有明显length、Unencrypted Header之类的常见特征 。总结来说，很难只依靠SS流量本身的特征来做检测识别，需要从上下文、流的外部和其他相关数据入手挖掘更多的信息来帮助检测。

然后开始提出新的解决思路，主要有三个点。
首先从数学的角度定义了Flow Correlation之类的概念，用于后面的数学建模和分析。

###### **Flow Context**

使用SS之后，不同流之间的关系有所变化。比如以前访问一个网页，要和web apge server、image server、video server、advertisement server分别建立连接。但是现在使用SS，这些连接被单一定向到为特定的SS server，由SS server代劳与这些服务器建立连接。显然，前者发散的流之间的关联与后者收敛的流之间的关联有很大的不同。

###### **Host Flow Behavior**

挂上了代理，产生的流量和访问的主机的数量和时长等也会有所变化，对外的连接没有之前那么发散和多样了，与之前有所区别。我觉得这里和第一点很相似，或者说关联度很大，可能因为噙着从Flow的角度出发，后者从Host的角度出发导致分析方法有所不同。

###### **Host DNS Behavior**

重点是PAC和部分全局模式下的DNS泄露问题。PAC模式使得对特定域名的访问才走SS,有时为了降低SS server的负载，Host会在本地请求域名的DNS，然后通过SS server来生成连接。那么这样一来，一是可以检测主机请求敏感域名的行为来判定，二是可以观察Host是否只请求敏感域名的 DNS但不立刻建立连接这种特别行为来判定。

### 写作技巧

> 跳出单一技术狂热的小圈子，把研究价值往更高的层面扩展

单纯从技术的角度来看，本文的摘要和引言篇幅显得有些臃肿。

摘要部分花了接近一半的篇幅来介绍SS的应用场景。

从VPS促进匿名通信聊到SS便利了非法网络活动，举例网络攻击和暗网交易，说明检测SS流量的必要。然后才落脚到SS技术的本身和之前的检测手段的局限之处。虽然这些都是事实，但行内人对这些东西都是非常清楚的，不必赘述，一句话点出即可，直接从之前检测手段的局限性开始，更有利于强调context flow 和 host behavior这两个创新点。

同样的，在introduction部分，也是花了一定的笔墨描述SS的违法利用方式，虽然比例不算太大，但考虑到内容与摘要部分有所重复，以及本文16页的长度与我等本科生孱弱的阅读能力，让人不由地感觉读了一页多，都还没搞清楚作者的意图，甚至连研究现状都没有了解到个大概。

综上，初次阅读觉得有些冗余，但是在读完全文之后才意识到这样做的合理之处。

除了新方法本身的先进性，作者先描述了这种方法的应用价值。即method based on flow context and host behavior可以有效地检测SS Flow，那么非常自然的，同时也与摘要和引言对背景的详细介绍相呼应的，就可以说有利于缓解SS使用者对VPS平台的滥用，进一步提升了云计算平台的安全性，同时也提升了network的安全性。这样一来，依赖于应用背景与应用价值提升了文章和技术的高度。

如果单纯就SS这一技术而言，本文提出novel method确实很有价值，它显示对技术的突破，但它的价值始终局限于SS这一技术本身。如果说联系SS的使用环境和detection的应用价值，则显示了新方法对保护VPS和检测恶意攻击的作用，从而提升到维护网络空间安全的这一更高的层面上来。即从检测SS匿名通信流量跳跃到提升网络空间安全层面。

当然，摘要和引言部分内容的重复和冗余仍然不可忽视，我只能认为这种做法利大于弊。

同时着也提示我在以后可能的写作中，要避免单一技术狂热，应当并重地考虑技术的应用价值，即同时体现技术的创新和应用的价值，使得理论与实践相结合。

### 缺陷

###### 略欠说服力的数据集

实验部分只使用了从校园网采集的流量，考虑到校园内网络使用者的身份相对比较单一，我在想是不是可能不会具有一般网络环境的一些Feature？如果这样的话，那么。

###### 2个VPS

同时一共才部署了两个VPS，那么要实现文章提及的对cloud computing platform的保护是不是就没有太大的说服力。

###### 回避问题

强调自己方法的进步，但对于新方法的可能的缺点却有所回避。（可以理解）

比如DNS泄露的问题貌似现在可以解决，而且从文章的描述来看，DNS泄露只在PAC和部分全局模式下会出现，那么对于使用没有DNS泄露的全局模式流量而言，是不是检测准确率会下降甚至比之前的方法还要低呢？

###### 进一步研究

个人认为这个工作还有进一步做下去的价值。

显然这篇文章可以为SS的作者提供改进迭代的灵感（虽然他早已删库跑路），那么可以怎么样改进来避免被检测？或者说本研究对设计加密通信协议有哪些启示？进一步，针对可能的改进，本方法又可以怎么样迭代来再次检测出它，或者有没有相对“一劳永逸”的机制来保证在一定时间内不会被绕过。如果这样提一下或者回答一下这些问题，可以彰显进一步研究的价值。
