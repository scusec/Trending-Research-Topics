##  *T-CAD: A threshold based collaborative DDoS attack detection in multiple autonomous systems*

> ### **论文信息**

&ensp;&ensp;**作者：** *Karanbir Singh, Kanwalvir Singh Dhindsa,  Deepa Nehra*

&ensp;&ensp;**出处：** *Journal of Information Security and Applications 51（2020）*

&ensp;&ensp;**链接：** *https://www.sciencedirect.com/science/article/abs/pii/S221421261930434X*

&ensp;&ensp;**笔记作者昵称：** *stone-coder/潘宏宇*


> ### **论文简要**

&ensp;&ensp;&ensp;&ensp;DDOS攻击近年来一直是个热门话题，它已经成为互联网服务提供商不可忽视的安全威胁。这篇文章提出了一种分布式攻击检测机制T-CAD，意图通过观察自治系统边缘路由器上的流量来检测和减轻DDoS攻击的影响，具体则是通过计算标准化的路由器熵，并将其与各种阈值进行比较，以此有效区分合法流量、DDoS攻击和flash事件。此外，这篇文章还利用omnet++和INET进行了仿真实验，以此验证了这个攻击检测机制的有效性。仿真实验结果表明，这个攻击检测机制在多个性能指标上优于现有的基于阈值和基于熵的DDoS攻击检测机制。


> ### **框图**

<img src="./DDOS defense architecture.jpg">

&ensp;&ensp;&ensp;&ensp;此图给出了这个T-CAD防御机制的详细架构，其可大致分为四个模块，具体为流结构模块、可疑活动检测模块、可疑流检测模块和DDOS攻击确认模块。

+ 流结构模块（Flow Construction）会解析由边缘路由器接收到的传入流量，并将其中的IP地址、端口号等报头特征提取出来，构造出新的流。

+ 可疑活动检测模块（Suspicious activity detection）会计算路由器的流量的归一化路由器熵(ne)，并与检测阈值(TD)匹配，当NE值小于检测阈值TD值时，确认其为可疑活动。

+ 可疑流检测模块（Suspicious flow detection）会计算边缘路由器的反向流中每个流的包速率(PR)，并与包速率阈值(TP)进行匹配，当PR值大于TP值，则则该流为可疑流。

+ DDoS攻击确认模块（DDoS attack confirmation）会计算当前路由器(ER1)和相邻路由器(ER2)的熵率，并将熵率(D)与熵率阈值(TE)进行比较，当D的值大于TE的值，该可疑流被确认是DDoS攻击流。
  
> ### **主要内容**

&ensp;&ensp;&ensp;&ensp;这篇论文首先介绍了DDOS攻击的原理和相关安全事件，然后综述了此领域的研究现状并说明自身的贡献，之后阐述了和研究内容相关的理论知识，又详细介绍了自己提出的T-CAD攻击模型（结构和工作原理），然后介绍了仿真实验及其实验结果，最后进行工作总结并进行展望。


> ### **创新点**

&ensp;&ensp;&ensp;&ensp;这篇文章区别于现有的基于熵和基于阈值的攻击检测机制，提出了一种新的基于熵和阈值的攻击检测机制，在多个性能指标上有更好的表现，并且能够精确识别DDOS攻击和flash事件。此外，这种攻击检测机制还具备低成本的特点，因为它可以很容易在边缘路由器上部署，最大限度地减少了硬件监控设备的数量。


>### **目前缺点**

+ T-CAD这种攻击检测机制虽然是一种低成本的解决方案，但是对于单个路由器来说，会消耗其大量的计算资源。

+ 这种攻击检测机制在不同环境的路由器部署时，其兼容性、协同性有所欠缺。
