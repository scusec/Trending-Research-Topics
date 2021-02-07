#SODA: A Generic Online Detection Framework for Smart Contracts
----
- 作者：Ting Chen (University of Electronic Science and Technology of China), Rong Cao (University of Electronic Science and Technology of China), Ting Li (University of Electronic Science and Technology of China), Xiapu Luo (The Hong Kong Polytechnic University), Guofei Gu (Texas A&M University), Yufei Zhang (University of Electronic Science and Technology of China), Zhou Liao (University of Electronic Science and Technology of China), Hang Zhu (University of Electronic Science and Technology of China), Gang Chen (Chengdu Kongdi Technology Inc.), Zheyuan He (University of Electronic Science and Technology of China), Yuxing Tang (University of Electronic Science and Technology of China), Xiaodong Lin (University of Guelph), Xiaosong Zhang (University of Electronic Science and Technology of China)
- 出处：NDSS
- 链接：[原文链接](https://www.ndss-symposium.org/wp-content/uploads/2020/02/24449-paper.pdf></https://www.ndss-symposium.org/wp-content/uploads/2020/02/24449-paper.pdf)

## 论文简要

区块链上的安全威胁层出不穷，并已经造成了严重经济损失。已有的离线方案无法保证发现所有的安全问题，也无法检测攻击；而已有的在线方案扩展性差、部署费用高、或无法检测某些攻击的问题。本文设计了针对智能合约的在线检测框架SODA，具有可扩展性好、运行速度快、兼容性好的特点。

## 框图

<img src=http://chuantu.xyz/t6/732/1588702891x992239408.png />

## 主要内容

作者提出并开发了一种新的用于检测各种攻击的通用在线检测框架SODA。SODA的性能、效率和兼容性优于现有的在线检测方法。本文还提出了按需信息索取，能够有效降低SODA的运行时开销。在SODA基础上，本工作实现了8款针对不同区块链安全问题的检测器。作者将SODA集成到三条区块链：Ethereum、Expanse和Wanchain上，并检测到大量的安全问题。此外，通过大量的实验发现，SODA加上8款检测器的运行时开销仅为25.5%，每笔交易检测时延仅为35微秒。

## 创新点

1、基于SPA，用户可以在几行代码中开发新的保护应用程序，而无需修改EVM，并轻松地将它们部署到区块链中。
2、设计了按需信息检索来减少信息收集的开销，并采用动态链接来消除进程间通信（IPC）的开销。它允许用户使用任何可以生成动态链接库（dll）的编程语言来开发保护应用程序。
3、SPA可以在不修改保护应用程序的情况下轻松迁移到此类区块链。

## 目前缺点

1、SODA不支持精确的数据流跟踪，因此应用程序可能会产生误报。
2、应用程序未同步运行，SODA无法停止执行有问题的智能合约。
3、缺少一种机制在区块链节点上部署SODA和应用程序，如果只有一个节点配备SODA或安装不同的应用程序，那么两个节点可能无法达成共识。
