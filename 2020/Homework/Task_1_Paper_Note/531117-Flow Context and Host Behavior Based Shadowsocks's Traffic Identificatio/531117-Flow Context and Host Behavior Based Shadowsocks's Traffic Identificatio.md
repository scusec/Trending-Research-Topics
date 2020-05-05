# 文章标题：

    Flow Context and Host Behavior Based Shadowsocks's Traffic Identification
    
    —— 基于流的上下文和主机行为的Shadowsocks流量检测方法

### 基本信息：

    文章为撰写的主体为四川大学的老师和同学，主题与shadowsocks的基于上下文的流量检测检测方法有关

###### 文章来源

    IEEE SPECIAL SECTION ON SECURITY AND PRIVACY FOR CLOUD AND IOT 2019

  +  https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8676111

###### 文章作者

    作者: XUEMEI ZENG , XINGSHU CHEN, GUOLIN SHAO, TAO HE, ZHENHUI HAN, YI WEN, QIXU WANG

 +   曾雪梅 			四川大学计算机学院
 +   陈兴蜀 			四川大学网络空间安全学院
 +   王启旭 			四川大学网络空间安全学院

###### 本文作者信息

    ababab
    一个闲散的无业吃瓜人员

### 文章概述

    因为shadowsocks的vpn加密通信被恶意利用于网络犯罪等违法行为，并且因为其加密的特性，导致对它的追踪和破译变得困难。论文作者为了解决相关的问题，在大量分析了早期研究基础和成果后，提出了based on flow context and host behavior（基于上下文、和行为）的识别方法，并通过基于the relationship between flows, hosts’ flow behavior, and hosts’ DNS behavior to build the detection model等方法建立了12维模型
    论文成果：通过在校园网和他们搭建的NTCI-BDP系统中进行测试，达到了93%准确率。并且该方法适合大规模网络，有利于维护Network和VPS平台的安全性。


###### 文章背景

 shadowssocks这种基于vpn的加密通信手段被滥用于网络犯罪等活动，严重威胁网络安全，同时也对VPS服务商有影响。

###### 问题分析及shadowsocks特征分析，并提出解决方案

    文章先介绍shadowsock的加密通信机制并分析其加密通信的特征，然后启开始分析具体的对其通信进行识别和解析的方法。
    本文从上下文分析、dns动作分析等角度提出了新的检测方法，并通过大数据分析和数据关联的技术来实现。该部分为文章的创新点所在。
    
    由于加密参数在部署SS server时预置，所以没有握手或者说协商加密参数的阶段。并且没有明显length、Unencrypted Header之类的常见特征 。总结来说，很难只依靠SS流量本身的特征来做检测识别，需要从上下文、流的外部和其他相关数据入手挖掘更多的信息来帮助检测。所以文章开始提出新的解决方法，主要通过三种途径。首先从数学的角度定义了Flow Correlation、Host Flow Behavior、Host DNS Behavior等的概念，用于后面的数学建模和分析。

 +  Flow Correlation
    在使用SS代理之后，不同流之间的关系有所变化。比如以前访问一个网页，要和web apge server、image server、video server、advertisement server分别建立连接。开启shadowsocks后，这些连接被定向到为代理用的SS server，由SS server作为代理人与实际被访问服务器建立连接。显然，前者发散的流之间的关联与后者收敛的流之间的关联有很大的不同。

 +  Host Flow Behavior
    开启ss之后，产生的流量和访问的主机的数量和时长等也会有所变化，对外的连接没有之前那么发散和多样了。（就实际效果而言，个人感觉和上面的区别不大）

 +  Host DNS Behavior
    该部分主要是PAC模式下（或黑白名单代理下）的DNS泄露问题。PAC模式使得其仅仅在特定的域名或地址访问时才使用代理,该设计主要是为了SS server的负载并提升访问当地网络的速度，主机会在本地请求域名的DNS，然后在SS server来生成连接。这样一来，就可以检测主机请求的域名的行为来判定，并且可以分析Host只请求敏感域名的DNS解析但不立刻建立连接的行为来判定。（但是这个办法貌似会对新的Firefox误判严重，因为它启用了新的加密dns机制，具体就不在这赘述了）

###### 文章总结

    本文通过实验对比表示本研究的方法可以更加准确的识别出ss流量特征，对维护网络的安全打击网络犯罪提供了有力的帮助，并且本方法也适用于大型网络种，呼应了前文中对背景和现状的阐述。

### 本文论述存在的一些缺陷

  1. 实验部分只使用了部分从校园网中采集的流量，因为该网络使用环境中的访问特征可能更加单一、流量特征不够多元话可能导致该方法的准确率虚高
  2. 本文为了验证是否对大型网络也能良好支持一共部署了两个VPS用于测试。但是感觉仅仅2个vps并不能称之为大型网络环境，对文章提及的对cloud computing platform的保护是不是就没有太大的说服力。
  3. 文章中无意识的回避了新方法可能存在的问题

 >   个人认为这个工作其实还要进一步改进和提升的可能。

    因为其实这种网络对抗是一个相互的过程。如果作者对当前的问题进行升级（虽然他已经跑路了）又怎么样来再次检测出它，或者有可以进行更深入的研究来发现一个shadowsocks实现上一些更无法避免的问题来长期化的解决识别ss流量的问题。
