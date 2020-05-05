## 论文信息

### 标题

A Collaborative Strategy for Mitigating Tracking through Browser Fingerprinting

### 作者 

Alejandro Gómez-Boix

Davide Frey profile imageDavide Frey

Yérom David Bromberg

Benoît Baudry

### 出处

MTD’19, November 11, 2019, London, United Kingdom c 2019 Association for Computing Machinery.

### 链接

https://dl.acm.org/doi/abs/10.1145/3338468.3356828

------

## 论文简要

这篇论文主要解决的问题在于浏览器特征指纹识别，通过提出一种新的方法想要解决网站通过用户的浏览器各种信息（如HTTP头文件、JavaScript）等识别出不同的用户，从而避免用户身份的泄露

------

## 框图

以下为该论文工作大致的流程：

![框图](https://raw.githubusercontent.com/Keshaun-Plus/lesson/master/01%20%E9%BB%84%E8%AF%9A/%E6%B5%81%E7%A8%8B%E5%9B%BE.bmp)



------

## 主要内容

通过这篇论文给出的数据显示，通过HTTP头等信息，以及启用的Flash或Java的配置信息中，可以有效的区分出不同的用户（在某些数据集中甚至高达94%）。而这篇论文想通过聚类等方法自动化的识别一组具有相似指纹的浏览器，然后通过配置将其移动到相同指纹上，再通过docker容器来虚拟化的运行web浏览器，从而在服务端看来，就会出现很多相同的浏览器指纹，使“相似的用户”变为“同一个用户”，从而降低网站通过浏览器指纹识别用户的可能性。

------

## 创新点

这篇论文的思想不是通过简单的限制对浏览器的配置信息的访问来隐藏用户的身份，而是企图通过修改不同用户间的配置信息，使相似的用户浏览器指纹相同，这样感觉比强行限制对浏览器指纹的访问更具有可行性。

------

## 目前缺点

我读了该论文之后主要有以下疑惑，首先是对浏览器指纹的修改会不会影响用户的使用；其次如果这项技术使用的用户不多，感觉“相似的用户”可能也不多，那么这样的隐藏是否有效果，用户数量的稀少是否会导致这项技术的实用性不高。