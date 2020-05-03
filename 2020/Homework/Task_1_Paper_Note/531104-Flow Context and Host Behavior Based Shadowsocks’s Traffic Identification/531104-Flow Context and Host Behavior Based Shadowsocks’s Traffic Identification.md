**论文标题**: Flow Context and Host Behavior Based Shadowsocks’s Traffic Identification

**作者**: XUEMEI ZENG  , XINGSHU CHEN , GUOLIN SHAO , TAO HE , ZHENHUI HAN , YI WEN , AND QIXU WANG 

**出处**: IEEE Access 

**链接**: https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8676111

**笔记作者昵称**:TomAPU

**论文简要**: Shadowsocks保护了使用者的隐私，也给网络审查造成了困难，因此需要找办法识别它。已有的方法要么对这种没有明显流量特征的通信协议无力，要么无法适应于大规模网络的环境。因此论文作者提出来基于寻找到的flow和flow之间，flow和host之间，flow和dns之间的12个特征，使用了随机森林算法来识别流量，准确率90%以上

**论文框图** ![JHqc5Q.png](https://s1.ax1x.com/2020/04/30/JHqc5Q.png)

## 内容

**背景**:SS的匿名性给网络审查造成了困难，现有的技术手段无法适用于大规模的网络环境，需要提出新的手段和方法

**相关研究**:

基于port和payload的识别：对SSL之类的有效，但是对SS这种无特征的无效

基于统计学的识别：能够识别Tor，但是针对SS还没有研究

基于流和主机行为之间的关联程度：效果不错，但是并没有关心流之间的特征

Gravitational Clustering Algorithm：成功识别了Tor

Draper-Gi 仅用基于时间的特征就能90%断定TOR

(但是他们都没研究SS)

2017年有人拿随机森林识别SS，但是并不适用于大型的网络环境


**这个研究的contributions**:

1.	找到了SS流量和非SS流量区别的特征：

- a)	Flow Context（流的关系
- b)	Flow Burst（和host behavior有关
- c)	Destination IP address Entropy（同上
- d)	Sensitive Domain Name（DNS特征
- e)	Unassociated Domain Name（DNS特征

2.	找到了新的探测SS的办法：

- a)	基于flow context and host behavior
- b)	用了big data statistics, association and data processing technology
- c)	适合large-scale network

3.	验证了方法的有效性

- a)	是目前最优的方法
- b)	从学校路由器(我校?)和标记的流量里面拿到的数据

**创新点**:
找到了12个特征,还建立了一个识别模型

**主要内容**: 
文章首先剖析了shadowsocks的通信模式，指出由于shadowsocks的特性，许多传统的方法无法提取特征进行识别，因此需要新的手段

因此文中从这几个角度分析

1. FLOW CONTEXT

-   如果挂上全局代理，那么不同流之间的相关关系发生改变

2. HOST FLOW BEHAVIOR

-   如果挂上全局代理，那么主机熵(host entropy)也会发生变化

3. DNS BEHAVIOR

-   SS的部分版本居然有DNS泄露，如果发现流量中有大量敏感域名，以及请求了DNS但是没有访问的域名，那就有可能是在用SS

在理论分析完，论证了可行性后。文章用了很mathy我看不懂的手段搞了很复杂的数学模型，基于以上的角度建立模型，然后根据从校园网路由器取下的流量进行分析，发现这个模型优于大部分方法，同时比别人的方法更加适合于大型网络环境

**缺点**: 

1. 和上面的两个角度不同，DNS泄露的缺陷更加容易被修补。事实上笔者亲测自己的SS并没有DNS泄露缺陷，证明了SS可能已经将这个缺陷修复，所以或许这个手段只能对特定的SS客户端奏效
2. 实验中使用了校园网来模拟大规模的网络环境，但是只选取了两个VPS来做实验，数量太少。
