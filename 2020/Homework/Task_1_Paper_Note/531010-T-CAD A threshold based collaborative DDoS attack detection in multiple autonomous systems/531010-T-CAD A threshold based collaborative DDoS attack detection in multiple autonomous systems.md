- 笔记作者：林逍逸

- 原文作者： Karanbir Singh  Kanwalvir Singh Dhindsa  Deepa Nehra

- 原文题目：T-CAD: A threshold based collaborative DDoS attack detection in multiple autonomous systems

- 原文来源：Journal of Information Security and Applications 51（2020）

  ##### 简述：
  
  DDoS攻击已成为对互联网服务提供商的安全威胁。 DDoS攻击对合法用户提供Internet资源和服务构成了巨大的威胁。 本文提出了一种称为T-CAD的分布式攻击检测机制系统，该系统通过观察自治系统边缘路由器上的流量来检测并减轻DDoS攻击的影响。  这篇文章利用omnet++和INET进行了仿真实验， 最终结果表明它优于基于熵的DDOS攻击检测机制。
  
  文章首先进行综述，然后介绍了传统的基于熵的检测机制的优缺点，再顺势提出了自己的T-CAD模型，分为模型介绍、模型工作方式详解、模型测试三个部分，给出了恰当的结论与讨论，最后给出了未来的工作总结和展望。



### 1、研究内容

###### 架构：

在架构介绍部分，可以笼统地概括为参数初始化、阈值识别、攻击检测算法三个部分

在T-CAD构造中，又分为四个部分。

 *Flow Construction* 、 *Suspicious activity detection* 、 *Suspicious flow detection* 、 *DDoS attack confirmation* ，构成了整个架构的环节。![1](C:\Users\Administrator\Desktop\531010-T-CAD A threshold based collaborative DDoS attack detection in multiple autonomous systems.md\1.jpg)

###### 数据：

参数初始化需要三个环节：  *Time window and sampling duration* 、 *Threshold values* 、Packet header features

###### 模型测试：

 OMNeT ++ ，是一个基于事件的离散仿真框架以及INET框架，用于测试所提出的攻击防御机制的效率。  INET支持将在互联网仿真中使用的协议（例如IP，TCP，UDP，网络层，传输层）。 ReaSE  是INET的扩展，通过保留链路带宽，节点和流量模式等现实网络方面的信息，用于生成现实的仿真拓扑。 

在结论部分的综合结果：

![2](C:\Users\Administrator\Desktop\531010-T-CAD A threshold based collaborative DDoS attack detection in multiple autonomous systems.md\2.png)

### 2、创新点

本文的主要创新点如下：

-  T-CAD以分布式方式工作，并在早期从多个来源消除了DDoS攻击的影响，与现存的基于熵的攻击检测机制进行比较，且显著更优。 
-  提议的DDoS防御系统的实际含义是可以在参与ISP的边缘路由器上轻松实现。 它帮助ISP为客户提供低成本的解决方案。
-  提议的防御机制可以以增量方式安装在多个自治系统上。 
-  在实际的仿真环境中，使用OMNeT ++和INET对提出的算法进行了验证。 

### 

### 3、论文评论

·论文在研究既有检测方式的基础上，进行了自己的数据实验分析，详实地提出了自己的观点，具备一定的参考价值。

·论文中没有明确阐述和分析新提出检测方法的缺点和不足，这是论文本身的一项重大不足。
