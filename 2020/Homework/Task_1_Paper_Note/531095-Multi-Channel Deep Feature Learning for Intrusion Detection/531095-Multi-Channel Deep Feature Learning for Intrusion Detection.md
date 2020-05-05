### 论文阅读笔记

#### **论文题目：Multi-Channel Deep Feature Learning foe Intrusion Detection**

#### **论文作者：GIUSEPPINA ANDRESINI, ANNALISA APPICE, NICOLA DI MAURO, CORRADO LOGLISCI, AND DONATO MALERBA (Member, IEEE)** 

#### **论文出处：https://ieeexplore.ieee.org/document/9036935/**

#### **论文主要内容：**

​		这篇论文提出了一种新的基于深度学习的入侵检测方法：多通道深度特征学习，并从多个数据集中收集数据来测试方法的有效性。作者通过结合**基于两个自动编码器神经网络的无监督多通道特征构造方法**和**利用跨通道特征相关性的有监督多通道特征构造方法**，来实现多通道深度学习入侵检测。本文的创新性在于将网络流量表示为原始数据向量，并以使用自动编码器来推导每个网络流量的多通道表示。

#### 可能存在的缺陷：

​		本文作者在神经网络中应用了自动编码器，将原数据先压缩到低维度然后反解回来，可以提高异常检测的准确率，但势必会导致CNN中的卷积核数量的增加，也就会导致训练一个模型花费的时间变长，占用更多的资源，特别是在层数较多的神经网络中。

