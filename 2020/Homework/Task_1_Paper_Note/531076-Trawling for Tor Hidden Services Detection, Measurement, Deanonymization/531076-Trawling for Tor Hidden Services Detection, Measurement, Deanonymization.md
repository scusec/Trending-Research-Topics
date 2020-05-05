### 论文基本信息

原文作者：{ [Alex Biryukov ](https://ieeexplore.ieee.org/author/37842357000); [Ivan Pustogarov ](https://ieeexplore.ieee.org/author/37671097300); [Ralf-Philipp Weinmann](https://ieeexplore.ieee.org/author/38110188900) }

原文题目：Trawling for Tor Hidden Services: Detection, Measurement, Deanonymization

原文来源： *IEEE Symposium on Security and Privacy* 

文章链接：https://ieeexplore.ieee.org/abstract/document/6547103

笔记作者昵称：Gossipboy

### 主要内容总结

Tor匿名网络为各种网络非法犯罪行为提供了极大的便利性，为打击此类非法行为，首先就需要进行溯源，这为溯源者带来极大的挑战。

架构：

 <img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/6547086/6547088/6547103/6547103-fig-1-source-small.gif" alt="图1" style="zoom:50%;" /> 

通过介绍Tor网络工作原理，即通过隐藏服务标识符来进行两端通信身份的确认，从此切入点进行考虑，进行爆破或者拦截工作，以此来溯源Tor网络中的使用人。

### 主要创新点

通过对Tor网络的隐藏标识符来进行溯源，并据此层层上溯，最终得到隐藏在网络背后的真人信息。

### 缺点

根据文章所述，作者使用的方法准确率很高，但具体如何做的并未提及，只是提到可以从标识符下手。不过，总的来说，能够做到对Tor网络的溯源，已经极其厉害了。但是文章就如何保证溯源过程中自身的安全性并未给出方案。
