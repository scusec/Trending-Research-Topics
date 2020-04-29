# Measuring the Deployment of Network Censorship Filters at Global Scale

## *笔记作者：网络空间安全学院 韩鑫华 2017141531056*

> **论文基本信息**
>
> 作者：Ram Sundara Raman, Adrian Stoll, Jakub Daleky, Armin Sarabi, Reethika Ramesh, Will Scottz, Roya Ensafi
>
> 单位：University of Michigan, {ramaks, adrs, arsarabi, reethika, ensafi}@umich.edu；The Citizen Lab, University of Toronto, jakub.dalek@utoronto.ca；Independent, willscott@gmail.com
>
> 出处：Network and Distributed Systems Security (NDSS) Symposium 2020
> 23-26 February 2020, San Diego, CA, USA
>
> 链接：https://dx.doi.org/10.14722/ndss.2020.23099

## 项目摘要

​		用于互联网审查的内容过滤技术面对一大难题，即只能较小范围内进行过滤，而且自动化程度低。本论文旨在提出FilterMap，一种基于全球视野对blockpage的部署进行半自动化检测的方法，为衡量整体互联网内容过滤情况有所帮助。

## 内容概要

1. ### 核心思想

   通过手动设置TCP/IP，HTTP等协议层的签名，检测那些在应用层通过对关键词及域名进行过滤的相关技术部署。

2. ### 传统技术的局限

   由于页面的动态性，针对页面长度和术语频率设置签名的效果误报率较高，且不具有较好的可扩展性，故不能应用于大范围的检测。

3. ### 本项目特点

   1. 可检测规模大
   2. 自动化程度高
   3. 鲁棒性较强（对抗测量伪影和噪声）
   4. 可同时分析历时性（纵向）和共时性（横向）数据

4. ### 主要原理图示

   1. 基础架构![](https://i.postimg.cc/BbRbLxbH/image.png)
   2. blockpage判断流程![](https://i.postimg.cc/xdjmS3z1/Hyper-Quack.png)
   3. 迭代分类算法![](https://i.postimg.cc/sgRQYQpy/Iterative-Clustering.png)

## 实验详细设计

1. ### 远程测量技术选择：[Quack](https://censoredplanet.org/projects/quack) & [HyperQuack](https://censoredplanet.org/projects/hyperquack)

2. ### 数据库选择：[CLTL](https://github.com/citizenlab/test-lists)

3. ### 数据收集模块

   1. 可用节点筛选：

      根据以下原则减少检测节点数量：位置多样性——尽可能有距离足够远且具有一致性的节点；伦理鲁棒性——不能影响到用户的正常使用。

   2. 审查过滤探测：

      通过HTTP（S）等协议包的相关字段以及页面显示，对访问结果进行收集。通过判断是否与模板预测的响应一致来确定敏感域是否存在审查过滤，具体流程如上。

4. ### 数据分析模块

   1. 迭代分类：通过手工标签将频繁出现的页面分成三类（blockpage；意外响应；无分类），降低数据维度。
   2. 图像聚类：对视觉要素进行分类，可对过滤类型进行初步筛选（本实验采用DBSCAN聚类）。

5. ### 实验设置

   ​	两个对照组：共时性（102个国家&33种）&历时性（从2018.11到2019.1，每14天为一组数据）

6. ### 实验结果

   1. 过滤类型：商业性部署；政府部署；互联网服务提供商部署；其他组织性部署
   2. 历时性数据：把握规避节点及监测节点的位置变化
   3. 与其他方法对比：Censys方法以IP地址作为检测基本单位，具有更完整的Internet视图且准确度较高，但可扩展性较低。

## 项目反思

1. ### 局限性：

   1. 由于受到节点选择的限制不能完全模拟用户的访问情况，与真实情况有所偏差；
   2. 检测精度为国家层面，只能粗略的部署情况；
   3. 主要对blockpage的返回页面进行签名设计，未深入到逻辑实现层面，无法进行更深层次的分析。

2. ### 可改进方面：

   1. 在返回页面之外用其他返回内容（如电子证书等）生成签名特征，识别过滤部署及深层逻辑实现；
   2. 对Censys与FilterMap进行综合对比，进行细粒度的检测单位设计。