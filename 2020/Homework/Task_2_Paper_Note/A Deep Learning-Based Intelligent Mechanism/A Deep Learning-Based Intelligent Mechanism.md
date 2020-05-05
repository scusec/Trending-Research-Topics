# Task2

- 笔记作者：weidu
- 原文作者：Youbiao He, Student Member, IEEE, Gihan J. Mendis, Student Member, IEEE, and Jin Wei, Member, IEEE
- 原文题目：Real-Time Detection of False Data Injection Attacks
  in Smart Grid: A Deep Learning-Based Intelligent
  Mechanism
- 原文来源 IEEE Transactions on Smart Grid, 8(5), 2505–2516. doi:10.1109/tsg.2017.2703842 

---

##论文主要内容总结（针对什么问题，做了什么工作，实现了什么目标等， 100-200字）

当今计算机技术和网络的普及提高了各个机构和设施的智能化效率，但是造成了过度的依赖，所以智能电网设置这种联网设备就更容易遭到攻击，本文利用深度学习技术利用历史测量数据来识别FDI攻击的行为特征，并利用捕获的特征来实时检测FDI攻击。本文提出的检测机制有效地放宽了对潜在攻击场景的假设，并实现了较高的准确性。
此外，我们提出了一种优化模型来表征一种FDI攻击的行为，检测损害了电力系统因窃电而导致的损失



## 论文主要创新点（50-150字）

利用深度学习技术利用历史测量数据来识别FDI攻击的行为特征

并利用捕获的特征来实时检测FDI攻击



## 论文的缺点（不少于50字)；

We would like to clarify that, although we consider one specific FDI attack

作者自己承认该模型只能针对一种FDI 攻击，适用面比较狭窄，如果多做研究可以将检测拓展到其他威胁检测

该论文的称述部分有过多的公式，而没有针对解决的问题进行详细的阐述，实用性较差



##解决该问题可能采用的其他替代方案或对本篇论文缺点的改进方法（200字以上，可分点陈述）；

文章采用的CNBD架构的模型不如使用SPN比如：

SPN的优势

比如RNN是一种链式的深度学习架构，它能够处理长时间序列，再此基础上又有其拓展出来的LSTM，BI-LSTM，GRU等等；而还有基于卷积核的深度学习架构比如CNN，TextCNN等，通过卷积核对输入数据进行扫描取得特征再进行池化等操作输出给后续的全连接层进行计算等。而SPN是一种基于图模型的，树形的深度学习架构。通过作者的实验可以看出，SPN在图像补齐等任务上明显优于基于CNN的架构。而且整个模型都可以使用统计理论来进行解释，它的计算复杂度也在多项式时间复杂度内。在某些任务中SPN架构可以作为一种深度学习架构的补充。

  
