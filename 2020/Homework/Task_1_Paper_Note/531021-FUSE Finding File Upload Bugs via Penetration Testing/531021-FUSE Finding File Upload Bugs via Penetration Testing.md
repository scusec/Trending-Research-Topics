#### 论文信息

- 标题：FUSE: Finding File Upload Bugs via Penetration Testing

- 作者：Taekjin Lee, Seongil Wi, Suyoung Lee† , Sooel Son†

- 出处：Network and Distributed Systems Security (NDSS) Symposium 2020 23-26 February 2020, San Diego, CA, USA

- 链接：https://www.ndss-symposium.org/wp-content/uploads/2020/02/23126.pdf

  


#### 论文简要

- 设计实现FUSE，一个可识别U(E)FU的渗透测试系统

- 设计突变操作改变标准上传请求，在不篡改上传请求的情况下，绕开内容过滤检查从而解决了实现FUSE过程中的两个技术挑战

- 对真实 Web 应用程序进行了 FUSE 评估，而证明了其通过文件上传查找代码执行漏洞的功效

- 本文论证了通过精心设计的突变操作进行有效的渗透测试是可行的，这种突变操作不会篡改种子文件的代码执行，但能够有效地绕过内容筛选检查。

  

#### 框图

- ![](https://pic.downk.cc/item/5ea2a9e5c2a9a83be571ffcb.jpg)

  

#### 主要内容

- 介绍威胁模型以及攻击者利用 FUSE 旨在查找的 U(E)FU 漏洞的具体功能。描述了系统查找 U(E)FU 漏洞的两个技术挑战，并总结了我们应对这些挑战的方法。

- 给出FUSE的基本结构，介绍三个组件的功能

- 介绍FUSE 流程：Specifying a Testing Campaign、Chain Coordination、Mutating and Sending Upload Requests、 Upload Validation、Uploading .htaccess

- 介绍初步研究得出的五个关键突变目标，总结了我们为解决这五个目标而设计的13个突变操作列表

  

#### 创新点

- 提出一种基于突变的新颖算法，用于生成引发 U（E）FU 漏洞的上传请求。

  

#### 目前缺点

- FUSE目前只定义了在实现内容筛选检查时引发常见错误的五个目标，实施了 13 个突变。我们承认，还有其他突变方法，以实现相同的目标。
- 软件中嵌入的这些约束由于更新而改变时，突变也应修改以反映这些更改。还未能实现自动提取这些执行约束和反射这些突变约束。
