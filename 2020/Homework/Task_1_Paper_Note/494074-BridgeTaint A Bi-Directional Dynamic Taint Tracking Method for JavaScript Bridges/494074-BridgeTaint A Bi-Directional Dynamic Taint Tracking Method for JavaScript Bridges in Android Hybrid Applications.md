-   原文题目：BridgeTaint: A Bi-Directional Dynamic Taint Tracking Method for JavaScript Bridges in Android Hybrid Applications
 -   原文作者：Junyang Bai, Weiping Wang, Yan Qin, Shigeng Zhang, Jianxin Wang, and Yi Pan
-   原文来源：IEEE Transactions on Information Forensics and Security, vol. 14, no. 3, pp. 677-692, March 2019
-   原文链接：https://ieeexplore.ieee.org/document/8410576

混合应用程序由于其跨平台功能和高性能而变得越来越流行。 这些应用程序使用Java脚本桥接通信方案进行交互在本机代码和Web代码之间建立连接。虽然通过启用跨语言调用极大地扩展了混合应用程序的功能，但桥接通信方案也可能导致一些新的安全问题，例如跨语言代码注入攻击和隐私泄漏。 本文提出了一种双向动态污点跟踪方法，用于检测混合应用程序中的桥接安全问题。 

### 1、论文简要

本文针对Android混合应用中桥接通信带来的安全问题，提出了一种可行的双向污点跟踪方法BRIDGETAINT。在此基础上，开发了一个污点跟踪系统BRIDGEINSPECTOR与一个桥梁安全测试基准BRIDGEBENCH。并且在Android市场用BRIDGEBENCH和真实的应用程序来测试BRIDGEINSPECTOR。结果表明，BRIDGEINSPECTOR能够有效地跟踪网桥通信中的数据流，检测混合应用中的真实漏洞。

### 2、主要内容
1、本文提出了一种新的方法来追踪混合应用程序的跨语言数据流和污染数据。与现有的静态代码分析方法不同，本方法动态记录通过网桥接口传输的敏感数据的污点信息，然后根据记录的JavaScript和Java数据之间的映射恢复相应数据的污点标签。

2、基于BRIDGETAINT，本文设计并实现了一个用于Android混合应用程序的跨桥数据跟踪和安全检测系统BRIDGEINSPECTOR。在BRIDGEBENCH和1172个Android market应用程序上的实验结果表明，BRIDGEINSPECTOR能够有效地跟踪bridge通信的数据流，同时还可以检测到其他针对混合应用程序的攻击。

3、本文使用Cordova为Android混合应用程序开发了一个网桥安全测试基准BRIDGEBENCH。BRIDGEBENCH包括38个测试应用，其中32个应用存在跨语言隐私泄露的风险，其他6个应用程序易受跨语言代码注入攻击，可以作为桥梁安全检测系统性能测试的基准。第一组样品1-32通过网络发送用户隐私，第二组样品33-38利用代码执行API直接处理插件获取的本机数据。一旦这些数据包含恶意代码，就会导致代码注入攻击。测试结果显示BRIDGEINSPECTOR成功检测到所有路径中跨语言隐私泄露和代码注入漏洞的所有不安全数据流。

### 3、创新点
针对Android混合应用中桥接通信带来的安全问题，传统模糊跟踪方法不能分析跨越语言边界的桥梁通信数据流，而本文提出了一种可以双向传播不同语言之间敏感数据污点标记的污点跟踪方法，并且在此基础上开发了一个污点跟踪系统与一个桥梁安全测试基准。

### 4、目前缺点

因为使用TaintDroid来执行Java污点跟踪，BRIDGETAINT不可避免地继承了TaintDroid的局限性。TaintDroid只跟踪直接将受污染数据分配给目标对象的显式数据流，而不跟踪控制语句（如条件分支）或隐式通道中的隐式数据流。所以BRIDGETAINT也无法防御前隐式流和隐式通道的攻击。

