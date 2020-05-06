## 论文信息

- 论文题目： `CDN Judo: Breaking the CDN DoS Protection with Itself`
- 作者：Run Guo, Weizhong Li, Baojun Liu, Shuang Hao, Jia Zhang, Haixin Duan, Kaiwen Shen, Jianjun Chen, Ying Liu
- 论文来源：`NDSS 2020`
- 论文地址：`https://www.ndss-symposium.org/ndss-paper/cdn-judo-breaking-the-cdn-dos-protection-with-itself/`
- 本笔记的作者：Gary

-----

## 简要

本文主要利用HTTP/2与HTTP/1.1协议实现的差异、CDN的转发规则、以及CDN入口IP（对客户端）和出口IP（对原始网站）的数量差异，揭示了可以通过合理构造请求，利用CDN完成对其上承载的原始网站发起DoS攻击的方法。

## 框图

```
        +--->   I.  Introduction
        |
        +--->  II.  Background and Threat Model
        |
root----+---> III.  HTTP/2 BANDWIDTH AMPLIFICATION ATTACK
        |
        +--->  IV.  PRE-POST SLOW HTTP ATTACK
        |
        +--->   V.  DEGRADATION-OF-GLOBAL-AVAILABILITY ATTACK
        |
        |                           +---> Severity Analysis
        |                           |
        +--->  VI.  Discussion -----+---> Causes and Mitigation
        |                           |
        |                           +---> Ethics and Responsible Disclosure
        |
        +--->VIII.  CONCLUSIONS
```

## 主要内容

内容分发网络（CDN）借助其全球分布的网络基础结构来提高网站的访问性能和可用性，这有助于在Internet上以CDN为基础的网站的蓬勃发展。由于CDN驱动的网站通常都在运营重要的业务或重要服务，因此攻击者最有兴趣拆除这些高价值的网站，从而以最大的影响力造成严重破坏。由于CDN凭借其巨大的带宽资源吸收了分布式攻击流量，因此CDN供应商一直声称他们为CDN驱动的网站提供了有效的DoS保护。

但是，本文发现，CDN转发机制中的实现或协议弱点可以被利用来破坏CDN保护。通过发送精心制作但合法的请求，攻击者可以对背后的Origin网站发起有效的DoS攻击。
特别是，在本研究中，我们提出了三种CDN威胁。
通过滥用CDN的HTTP / 2请求转换行为和HTTP POST前行为，攻击者可以使CDN-Origin带宽饱和，并耗尽Origin的连接限制。

更令人担忧的是，某些CDN供应商仅使用一小组流量转发IP且IP转换率较低的IP来建立与Origin的连接。通过仅切断特定的CDN来源连接，此特征为攻击者提供了一个极大的机会，可以有效地降低网站的全局可用性。

## 创新点

- 攻击的角度十分地新颖
- 意图提高各个CDN厂商的警惕
- 直接在实际环境中进行了测试，实验数据更可靠

## 目前缺点

- 攻击思路被本文披露后，某些非顶级CDN企业或对安全不重视的网站管理员（CDN用户）可能会遭受到这些新型的攻击
- 列举了3种攻击方法，但可能还有其他方法未被发现或指出
