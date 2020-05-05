- 笔记作者：LydiaLee
- 原文作者：Nur, Abdullah Yasin, and Mehmet Engin Tozal.
- 原文题目：Record route IP traceback: Combating DoS attacks and the variants
- 原文来源：*Computers & Security* 72 (2018): 13-25.

Dos攻击和DDos攻击是当前互联网上最危险的威胁之一，尤其利用僵尸网络之后，使控制机更难以追踪。在本文中，利用IP协议的特征，使用概率包标记（probabilistic packet marking）方法，受害主机通过构造转发路径拓扑图，实现了使用少量接收到的攻击数据包来追溯到控制机。

### 1、研究内容

在本文中，使用了概率包标记的方式，通过在IP包中的options field添加标记位，解决了传统仅依赖于数据包中route option（在IP包的可选字段）存储转发路径时存储地址数目的限制。受害主机victim使用收到的数据包，分析route option字段和options字段，重新构建路由拓扑图，从而实现对attacker的追溯。

- #### 概率包标记 Probabilistic packet marking

  概率包标记是指路由器有一定概率将其地址插入到IP数据包中。在一般情况下，这些地址存储在IP数据包的可变部分。由于字节限制，最多只能存储9个地址，当转发路由大于9个时，就会有路由地址无法被记录的情况。

  在本文中，引入了标记位的方法。定义了ERR（essential record route）数据包。标记规则如下：

  <img src="C:\Users\lxs08\AppData\Roaming\Typora\typora-user-images\image-20200315114908240.png" alt="image-20200315114908240" style="zoom:50%;" />

- #### 构建路由拓扑图

  对收到的数据包进行解析分析，构建有向图来追溯attacker。构建方法如下：

  <img src="C:\Users\lxs08\AppData\Roaming\Typora\typora-user-images\image-20200315115558657.png" alt="image-20200315115558657" style="zoom:60%;" />

- #### 实验结果比较

  相比于**Fast internet traceback(FIT, 2005)**、**Authenticated marking scheme(AMS, 2001)**、**Fragment marking scheme(FMS, 2001)**，本文中的方法仅需要平均22.23个数据包就可以进行追溯，效率更高。

  <img src="C:\Users\lxs08\AppData\Roaming\Typora\typora-user-images\image-20200315120030609.png" alt="image-20200315120030609" style="zoom:60%;" />

### 2、创新点

本文的主要创新点如下：

利用了IP数据包中的option字段，弥补了只使用route字段带来的记录地址数的限制。

### 3、论文评论

本文使用了标记位的方法来标记不同类型的数据包，在实验环境下取得了很好的溯源效果。同时不需要对协议本身进行修改，适用于现在的IP协议。但是存在以下限制：

- 需要路由器供应商的支持，在路由器中加入修改标记位的功能，需要一段时间才能实现这种路由环境的构建。
- 本文中的方法是在发生攻击后进行溯源，在实际环境中攻击者可以在攻击后修改IP而逃避。如果需要应用在实践中，则需要构建更为快速的发现攻击和响应机制，才能够更具有实用性。

