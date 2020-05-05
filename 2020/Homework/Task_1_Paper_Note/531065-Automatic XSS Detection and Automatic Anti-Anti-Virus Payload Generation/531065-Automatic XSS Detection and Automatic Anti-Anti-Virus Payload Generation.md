# xss attack detection

* 论文基本信息

  > L. Li and L. Wei, "Automatic XSS Detection and Automatic Anti-Anti-Virus Payload Generation," 2019 International Conference on Cyber-Enabled Distributed Computing and Knowledge Discovery (Cyber C), Guilin, China, 2019, pp. 71-76.
  >
  > 链接：https://ieeexplore.ieee.org/document/8945988/keywords#keywords

  

* 主要内容

  > ​		文章针对XSS攻击，利用SVM算法建立了一个更有效的XSS自动检测工具、利用DQN算法来创建一个更有针对性的自动反病毒有效负载生成工具，此外还探讨了使用LSTM自动生成XSS攻击语句的方法。
  >
  > ​		文章首先介绍了XSS的原理以及它的绕过方式。然后依次介绍以上三种工具的实现：针对XSS自动检测工具，依次进行数据收集降噪标记、向量化、训练和测试；针对自动反病毒有效负载生成工具，它的目的在于绕过特定的规则WAF，既可以用于找到特定WAF的绕过方式，也可以用于安全性的评估；针对自动生成XSS攻击语句工具，文章只是做了简要的说明。

  

* 关键字

  >XSS攻击，自动检测，自动旁路，机器学习，强化学习

  

* 框图

  >如图1
  >
  >![1588135147073](C:\Users\HUWEI\AppData\Roaming\Typora\typora-user-images\1588135147073.png)

  

* 创新点

  > 相对于手动检测和源代码审核这两种既困难又效率低下的检测方法，以及常用的自动检测工具在具有不同防御规则的平台使用相同的测试数据而导致漏洞的漏失率和误报率较高等问题，文章中提出的方法可以实现动态的检测。

  > 文章详细的介绍了可能XSS攻击语句具有的特点: 通常恶意语句比正常请求语句长度长; 恶意语句通常包括HTML代码或JavaScript代码的关键字；恶意语句通常包括特殊字符；恶意XSS攻击语句中的第三方域名比正常语句中的域名要多；语句最后一个字符判断

  

* 缺点

  > 文章最后对于用RNN-LSTM算法自动生成XSS攻击码的方法描述只有短短的一小部分，并没有做和上面一样详细的阐述，也没有说明和上述提出的方法之间的关系。
  
  > 文章有一段内容是完全重复的，缺乏严谨性。
  >
  > 如图2
  >
  > ![1588136023327](C:\Users\HUWEI\AppData\Roaming\Typora\typora-user-images\1588136023327.png)

