# 论文信息

标题：Browser-Based Deep Behavioral Detection of Web Cryptomining with CoinSpy [[paper](https://www.ndss-symposium.org/wp-content/uploads/23002-paper.pdf)]

作者：C. Kelton, A. Balasubramanian, R. Raghavendra, M. Srivatsa

出处：NDSS Symposium 2020, Measurements, Attacks, and Defenses for the Web (MADWeb) Workshop 2020

链接：https://www.ndss-symposium.org/wp-content/uploads/23002-paper.pdf

笔记作者：IzaiahSun

# 论文主要工作

## 研究背景

近期浏览器端的加密货币挖掘（cryptojacking）得到了广泛关注，浏览器端加密货币挖掘包括了Web服务端向客户端发送的Cryptocurrency挖掘脚本，然后客户端进行分布式挖币。有些Web服务器运营商将这个作为广告的替代品，一定程度上改善用户的浏览体验。但是这种挖矿脚本大量占用了用户资源，并且可能在未经用户同意的情况下被部署并运行，因此有必要来对这类脚本进行检测。

## 本文贡献

- 提出了CoinSpy，一种完全基于浏览器的框架，结合了网页上执行加密挖矿脚本时的个各种信号，使用深度学习管道，来检测网页中的加密活动
- CoinSpy仅仅使用浏览器沙盒中能够获得的有限信息，对挖矿行为进行检测。

## 框架设计

![基本框架图](https://www.izaiahsun.com/wp-content/uploads/homework/new-technique/1/1.png)

该框架以CoinSpy插件为中心，CoinSpy插件首先从CoinSpy服务器接收模型，使用浏览器提供的系统数据，包括内存使用，CPU占用和网络占用。CoinSpy使用这些信息创建时间序列。这些数据被输入CNN中进行识别，如果识别出新的样品给CoinSpy服务器，服务器会使用新的样本更新模型，插件会定期更新来获得更新的模型。

## CNN网络

![CNN网络](https://www.izaiahsun.com/wp-content/uploads/homework/new-technique/1/2.png)

此处使用的CNN网络在输入经过一层一维卷积，一维池化之后，进入深度网络，多层卷积，多层池化之后全连接，使用softmax进行处理，最后输出一个可能性。

## 数据集来源

由于NoCoin和Outguard提供的数据量极少，而且很多网站都不存在了，这边使用了注入方法（Injection method），在网站里注入了coinhive.min.js，但是在后面的验证过程中，使用了其它家族的挖矿脚本。然后为了模拟实际环境，在生成数据的时候不断改变了CryptoNight PoW算法的参数。

## 模型表现

在验证过程中，使用了不同类型的设备，运行在不同设备上的模型没有被单独训练过，而是使用的通用模型。

| Metric      | Cloud Devices | Desktop Devices |
| ----------- | ------------- | --------------- |
| Accuracy    | 0.973         | 0.964           |
| Sensitivity | 0.970         | 0.982           |
| Specificity | 0.977         | 0.947           |
| BCR         | 0.973         | 0.964           |

除此之外，还对比了CoinSpy和其它检测方法的效果差别

| Miner               | CoinSpy | CMTracker | Outguard |
| ------------------- | ------- | --------- | -------- |
| CoinImp(Monero)     | 1.00    | 0.82      | 1.00     |
| CoinImp(WebChain)   | 0.98    | 0.84      | 1.00     |
| Crypto-loot(Monero) | 1.00    | 0.82      | 1.00     |
| Crypto-loot(uPlexa) | 0.98    | 0.84      | 1.00     |
| WebMine(Monero)     | 1.00    | 0.82      | 1.00     |

| Metric      | CoinSpy | CMTracker | Outguard |
| ----------- | ------- | --------- | -------- |
| Accuracy    | 0.95    | 0.73      | 0.98     |
| Sensitivity | 0.938   | 0.666     | 0.988    |
| Specificity | 1.0     | 1.0       | 0.95     |
| BCR         | 0.969   | 0.799     | 0.969    |

除此之外，随着CPU节流率的增加，CoinSpy的表现明显好于另外两种模型

![CNN网络](https://www.izaiahsun.com/wp-content/uploads/homework/new-technique/1/3.png)

# 未来研究

- 评估PoW算法上的增量学习
- 根据客户机算力来使用不同类型的神经网络架构，还有为了性能可能使用Tensorflow Lite这样的自动化框架来优化模型及其大小
- 计划评估CoinSpy浏览器扩展程序的用户统计数据，比如有多少用户能够为我们提供目前错过的挖矿网站的页面
- 一旦检测到加密货币挖掘行为，哪些行为可以从浏览器执行，那些应该从浏览器执行，这些都没研究，目前主要重点还集中在检测