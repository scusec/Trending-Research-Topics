-   笔记作者：Zhang Rukai
-   原文作者： Wenbin Yao, Yuanhao Ding, Xiaoyong Li
-   原文题目：Deep Learning for Phishing Detection
-   原文来源：2018 IEEE Intl Conf on Parallel & Distributed Processing with Applications, Ubiquitous Computing & Communications, Big Data & Cloud Computing, Social Computing & Networking, Sustainable Computing & Communications
-   论文链接：[论文链接](http://182.150.59.104:8888/https/77726476706e69737468656265737421f9f244993f20645f6c0dc7a59d50267b1ab4a9/stamp/stamp.jsp?tp=&arnumber=8672219)

如今移动互联网蓬勃发展，越来越多的公司选择使用二维码代替传统的URL用来推广自己的产品，以便在移动使用场景下方便用户，也能节省推广成本。但与曾同时，攻击者也注意到这种趋势，利用基于嵌入企业logo的二维码进行钓鱼攻击。本文提出了一种添加了改进FPN的Fater R-CNN进行嵌入logo的二维码钓鱼攻击检测。

### 1、研究内容

架构：整个检测过程从带logo的QR码出发，首先利用QR码的查找模式和纠错级别提取嵌入其中的logo，再利用添加了改进的特征金字塔网络的Faster R-CNN进行logo识别，最后利用数据库中合法域名的URL和目标logo的URL进行比对来识别目标QR码的合法性。研究架构图如下所示：

<div align=center><img src="http://m.qpic.cn/psc?/1e9d7ab3-d380-4dac-bbeb-131d4416bee9/OO0GOkEvd.dIewPrYqD0Dpj.xavVVMnKzbUqSWD9mYwqsGMwOXuzuPAxYi8dkuuaBF35LSgen4gDDwZv3VHn3Q!!/b&bo=zwQUAc8EFAEDCSw!&rf=viewer_4"></div>

<div align=center>图1 论文研究架构</div>

模型：检测模型是添加了改进的特征金字塔网络(FPN)的Faster R-CNN，每层都会在连接到上一层的特征映射，并且添加了子像素卷积层，如图2：

<div align=center><img src="http://m.qpic.cn/psc?/1e9d7ab3-d380-4dac-bbeb-131d4416bee9/gliYV*h0f2f2HjcOdYSYvXsDfejCJF26ObWyeui488dncpaEWg2PR1x3I.bp9uzG3oyfDimgFGCjf5*Goc3B.gK*12wZrANH92WN2KMzOcc!/b&bo=qARgAagEYAEDORw!&rf=viewer_4"></div>

<div align=center>图2 子像素卷积层</div>

整个神经网络共四层，除第一层外每一层都会以上一层的最后一层输出作为特征映射的参考集，以后三层形成三个融合层。神经网络结构如图3：

<div align=center><img src="http://m.qpic.cn/psc?/1e9d7ab3-d380-4dac-bbeb-131d4416bee9/gliYV*h0f2f2HjcOdYSYvXR9XaKbhVfWYKeblWqCE2Gby4Nfn4asJBf9ieRSonpk1FVs48mA0DQuXVBN87eVjyzRPSbim2Kvr5H9YnII2oU!/b&bo=hwP4AocD.AIDGTw!&rf=viewer_4"></div>

<div align=center>图3 神经网络结构</div>

数据：论文主要使用两个数据集：一个是包含32个不同品牌logo的开源数据集FlickrLogos-32，另一个是FlickrLogos-32plus，后者在前者的基础上进行了扩充，以满足实验对小尺寸目标检测的数据量的需求。

结果：

logo识别的结果以精确率、召回率和F1分数作为评价标准，分别展示了两个数据集的实验结果，如图4、图5：

<div align=center><img src="http://m.qpic.cn/psc?/1e9d7ab3-d380-4dac-bbeb-131d4416bee9/gliYV*h0f2f2HjcOdYSYvbzrnGllFvbMKoTEB8ihx9LnU1rArPoSI*2UYK0gELYKcf4mHftjshGgQ2.eeM80W..STBLZsdElYPzj3w1u1tg!/b&bo=UQPnAFED5wADGTw!&rf=viewer_4"></div>

<div align=center>图4 FlickrLogos-32数据集上的实验结果</div>

<div align=center><img src="http://m.qpic.cn/psc?/1e9d7ab3-d380-4dac-bbeb-131d4416bee9/gliYV*h0f2f2HjcOdYSYvV8*uO77Oyy8ld5ZftsGZtH.CEQ3AcCGl*PUsirvVrbcsnMpe.uGlGBvYf9MJhjHR2ZXsIj6.*26wquw.OJssyA!/b&bo=SwPlAEsD5QADGTw!&rf=viewer_4"></div>

<div align=center>图5 FlickrLogos-32plus数据集上的实验结果</div>

钓鱼攻击检测的精确度达到91.4%，召回率达到98.3%，F1分数达到94.7%，效果很好。实验结果如图6所示：

<div align=center><img src="http://m.qpic.cn/psc?/1e9d7ab3-d380-4dac-bbeb-131d4416bee9/OO0GOkEvd.dIewPrYqD0DthfJ.9CcEI1kxwzdhlfTsVGqjzLHAoHnnxdTjlT7ueMNNtyXW94n4HSTzeJ9SwHzg!!/b&bo=eAKaAHgCmgADCSw!&rf=viewer_4"></div>

<div align=center>图6 钓鱼攻击检测结果</div>

### 2、创新点

本文的主要创新点如下：

-   针对logo嵌入的二维码而不是传统的URL进行钓鱼攻击检测
-   使用的Faster R-CNN增加了一个改进的特征金字塔网络，并且添加了子像素卷积层
-   基于开源数据对数据集进行扩充，保证了实验结果的可靠性

### 3、论文缺点

文章的标题不够准确，没有突出作为研究对象的嵌入logo二维码。所使用的数据集尽管经过扩充，但数据量还是不够大，导致了实验结果可能与真实情况有一定偏离。Faster R-CNN层数不多，可以再适当添加层数。