* 笔记作者：欧远晨

* 原文作者：Qi Wang , Wajih Ul Hassan , Ding Li , Kangkook Jee , Xiao Yu，Kexuan Zou , 

​					  Junghwan Rhee , Zhengzhang Chen , Wei Cheng , Carl A. Gunter , Haifeng Chen 

* 原文题目：You Are What You Do: Hunting Stealthy Malware via Data Provenance Analysis

* 原文来源：NDSS Symposium 2020 Programme

随着恶意软件技术的更新，恶意软件比以前更加隐蔽难以发现，传统的恶意软件扫描工具已经无法完成对恶意软件的溯源。本文中，作者提出了一种基于源的恶意软件分析方式，基于神经网络构建了恶意软件检测模型。

#### 1、研究内容

正常软件与恶意软件的工作模式：恶意软件特殊的工作模式使得种源分析和跟踪技术检测隐身恶意软件的关键

![alt image](https://pic.downk.cc/item/5e9efca5c2a9a83be5b6ee69.png)

模型：

通过建立图，选择代表数据嵌入等步骤识别出恶意软件进程

![alt image2](https://pic.downk.cc/item/5e9f006bc2a9a83be5b9ab26.png)

数据集：收集了 23 个目标程序的良性来源数据， 并使用 Provector 建立了它们的检测模型。 然后用 1150 个隐身模拟攻击和 1150 个良性程序实例（每个目标程序 50 个）

评估结果：

使用了两个指标：精度，召回率

并计算了平均值F1-Score

![alt image3](https://pic.downk.cc/item/5e9effdec2a9a83be5b9469f.png)

评估结果表明该检测模型在检测隐身恶意软件达到了很高的精度，使用这个模型的检测能够达到平均精度0.959，平均召回率0.991

#### 2、创新点

* 使用因果路径分离源图的良性部分以及恶意部分
* 使用了一种只有ci图的新型路径选择算法，减少了训练检测工作量

#### 3、论文评论

在本文中作者提出了一种全新的基于源分析的恶意软件检测模型，实现了检测新型隐身恶意软件的高精度，具有很高的实用性。但目前本模型只提供了静态的检测，数据来源也仅限于Windows系统，没有从其他系统源获得数据，并且数据来源可能存在数据污染的问题。这篇论文的相关技术仍然有很多可以提高的空间
