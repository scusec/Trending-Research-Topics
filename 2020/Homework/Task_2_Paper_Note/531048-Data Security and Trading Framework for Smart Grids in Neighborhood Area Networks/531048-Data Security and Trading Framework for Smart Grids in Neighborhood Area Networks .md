# <center>论文笔记</center>
## 论文信息
### 论文标题：
Data Security and Trading Framework for Smart Grids in Neighborhood Area Networks  
城区网络中的智能电网数据安全和交易框架

### 论文作者：
Jayme Milanezi Junior， João Paulo C. L. da Costa， Caio C. R. Garcez，Robson de Oliveira Albuquerque，Arnaldo Arancibia，
Lothar Weichenberger，Fábio Lucio Lopes de Mendonça，Giovanni del Galdo， Rafael T. de Sousa,Jr
### 论文出处：
Sensors 2020, 20, 1337
### 论文链接：
`https://www.mdpi.com/1424-8220/20/5/1337`
## 论文概要
本文提出了一种针对Neighborhood Area Network(NAN)中智能电网保护用户隐私数据的方案。能够有效防御面向智能电网的流量分析攻击。
## 主要内容
在智能电网中，最为重要的需求之一就是终端用户的隐私安全，在本文中，作者提出了一种保护智能电网消费者身份隐私和抗流量分析攻击的框架。同时该框架能够向恶意攻击者隐藏智能电网中的竞标者以及竞标信息。该框架基于一种专用的通信系统实现通讯链路，为了确保数据安全，在信息传输过程中对信息实现了AES加密，密钥为长度128位的异或密钥。确保了安全性的同时保证了系统的计算复杂性较低，保证了系统运行的性能。相对其他的解决方案，该框架更好的实现了隐私保护和交易灵活性。
#### 以下为面向隐私保护的数据加密的示意图：
![avatar](https://s1.ax1x.com/2020/04/25/JyM9bT.png)
在该框架中，作者试图提供一个NAN中有效的消费者隐私保护方法，同时利用一种透明计价机制来允许每个智能电表记录交易的电量和对应的电价，在计价过程中，确保所有信息的机密性。
## 论文创新点
在智能电网系统中引入密码学机制，使用的密钥基于LFSR的异或矩阵，确保了数据的安全性。
## 目前缺点
128位的密钥对于AES而言，容易被暴力破解，同时在信息传输过程中，没有针对重放攻击等密码学攻击方式进行相对应的设计。
#### 笔记作者：
531048
