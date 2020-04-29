标题、作者、出处和链接、笔记作者昵称、论文简要、框图、主要内容、创新点、目前缺点

# Active Defense-Based Resilient Sliding Mode Control Under Denial-of-Service Attacks

Chengwei Wu , Ligang Wu , Senior Member, IEEE, Jianxing Liu , and Zhong-Ping Jiang

IEEE TRANSACTIONS ON INFORMATION FORENSICS AND SECURITY, VOL. 15, 2020



### 论文简要

​	   这篇文章通过创建一种弹性的控制机制来有效应对目标为物理设备DDoS攻击（主要控制逻辑框架如下文框图）。该研究的混合机制基于零和博弈论，同时，在效果评估上，研究尽力做到与真实场景接近的测试方案，结果表明弹性控制方法具备有效性。

### 框图

![image-20200422172922580](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20200422172922580.png)



### 主要内容

​		弹性控制系统以这个公式为主：

​			![image-20200422205716268](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20200422205716268.png)

​		以框架图的流程来说，攻击者通过僵尸主机向物理器发送Dos攻击时，攻击包首先会通过detector，detector会对这个请求进行判断，请求会被分解成y和x，分别表示攻击状态（1表示正常状态，2表示攻击状态）和时间戳。通过如如图的三个开关进判断，将最终通过判断的请求发送到执行器，最后发送给传感器。



### 创新点

1、该论文将Dos攻击刻画成一个物理事件，并将其比喻成开关，以开关表示Dos攻击成功还是失败，以及攻击的频率和持续时间

2、该研究引入了一种估计器来估计攻击所造成的损失

3、这是一种主动的防御策略，基于零和博弈的开关逻辑防御措施



### 缺点

1、考虑的受攻击场景不全面。只考虑到了传感器攻击，有些物理器件的状态没有考虑到，此类方法可以扩展到多类网络应用防护中。

2、考虑的攻击场景不全面。

3、效率问题。真实场景中面对大量的判断能否保障通讯效率的较小降低。