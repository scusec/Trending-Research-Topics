[TOC]

##  1.论文信息

标题：FUSE: Finding File Upload Bugs via Penetration Testing

作者：Taekjin Lee, Seongil Wi, Suyoung Lee, Sooel Son

出处：NDSS Symposium 2020 Programme

链接：https://www.ndss-symposium.org/ndss-paper/fuse-finding-file-upload-bugs-via-penetration-testing/

## 2.论文简要、框图及主要内容

​    UFU： Unrestricted File Upload 不受限制的文件上传

​    UEFU： Unrestricted Executable File Upload 不受限制的可执行文件上传

​    随着网络应用的不断扩大，很多web应用都有了文件上传功能，由此引发了种种潜在漏洞——比如UFU、UEFU等。该论文旨在描述一个渗透测试工具FUSE，通过构造上传请求来测试web应用服务器是否存在上述漏洞。

​	FUSE渗透测试工具需要满足两个条件：

​		1. 生成一个上传请求，该请求绕过目标web应用程序中存在的内容过滤检查，从而实现成功的上传

​		2. 需要成功地在目标web服务器或浏览器上上传可执行文件并保留其执行语义

​	由于很多web服务端都有一定的过滤措施，例如不允许“.php”后缀的文件上传等，因此渗透测试工具需要对上传请求进行一定的变种（FUSE总共定义了13种变种方法，并将其进行排列组合生成一条条“突变链”），尝试绕过这些防御措施来成功上传文件的同时保留执行语义、并且获取到该文件的URL。

如图所示：

![](https://pic.downk.cc/item/5e8058bc504f4bcb042b806e.jpg)

​	该渗透测试工具检测出了多个web应用的CE、PCE漏洞（在33个PHP应用中发现了30个UEFU漏洞，其中包括了15 CVE），同时，浏览器软件的不同版本对测试的结果几乎无影响，说明FUSE的实用性极高；相比于如今较为流行的其他渗透测试工具，FUSE的表现具有更大的优势、发现了更多的漏洞。

## 3.创新点

 1. FUSE分为三个模块：CHAIN COORDINATOR, UPLOAD AGENT, and UPLOAD VALIDATOR；每个模块负责完成相应的任务。CHAIN COORDINATOR对种子文件准备突变方法链，即规定了针对每个种子文件应当如何采取突变措施；UPLOAD AGENT负责生成上传请求并且执行相应的突变措施；UPLOAD VALIDATOR负责检测是否上传成功、获取文件的URL并测试是否可执行。

 2. CHAIN COORDINATOR这个模块是FUSE的创新点之一。FUSE总共定义了13种变异方法（M1 - M13），不同的文件类型有不同的变异方法选择。CHAIN COORDINATOR首先将所有可选操作进行排列组合，例如{∅,M1,M2,M3,M1M2,M1M3,M2M3,M1M2M3} ；第二步则是对该链进行清洗，删除相互之间有冲突的突变方法的组合；在应用突变方法链时，根据上述例子的顺序（即从短到长）来依次进行，如果M1成功引发了UFU漏洞，就会将在其之后的所有包含M1的突变组合删除，以此保证每次执行的操作是最短的组合从而压缩测试时间保证执行效率。

 3. 针对文件上传的HTTP请求的数据包内容进行操作。

    如图所示：

    ![](https://pic.downk.cc/item/5e805f67504f4bcb0431772b.png)

    ​	即(1) Extension

    ​		(2) Content-Type

    ​		(3) Content
    
    ​	这样的方法容易实现，并且较为简单，将上述定义的13种图片方法应用于此并在客户端生成相应的上传请求发送至服务端。

## 4.目前缺点

1. 随着PHP解释器的更新换代，FUSE也需要随之进行更新（如PHP文件扩展名等）
2. FUSE共定义了13种变异方法，但是有可能会有更多的其他方法未涉及到
3. 需要一种方法来自动提取出执行约束
4. 在报告相应漏洞后，有的供应商并未提供相应补丁，理由是这些漏洞需要管理员权限才能利用；我认为应当同样引起重视，因为有可能黑客先获取管理员权限，再利用漏洞。

