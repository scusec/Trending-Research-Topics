## PMTP: A MAX-SAT-Based Approach to Detect Hardware Trojan Using Propagation of Maximum Transition Probability

*   这是一篇关于硬件木马检测的文章，发表在 [IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems](https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=43) ( Volume: 39 , [Issue: 1](https://ieeexplore.ieee.org/xpl/tocresult.jsp?isnumber=8939296) , Jan. 2020 )上
*   作者：伊朗德黑兰大学的教授Ahmad Shabani

----

1.  作者提出了一种新的方法PMTP(propagation of maximum transition probability)来判断硬件木马。大致是针对单一的双入门电路（如与门、或门、异或门等等）进行出口和入口的检测，当门电路的状态和常规的概率分布不同时，则可以判断出异常，以此来快速判断硬件木马
2.  其主要的贡献即上述提到的PMTP方法，作者针对不同的门电路进行大量的测试，并绘制了transition probability关于门电路入方向为1的概率的三维图像，在transition probability最高时，用类似差分分析的方式来进行木马检测。这种检测方法的速度相比原来的方法快了很多。
3.  本文章的方法使用了部分密码学的思想，通过最高概率的传播来进行硬件木马的检测，然而，在作者的研究中，其针对单一门电路的通过概率最高仅为25%，在穿过大量门电路的情况下效果较差。

