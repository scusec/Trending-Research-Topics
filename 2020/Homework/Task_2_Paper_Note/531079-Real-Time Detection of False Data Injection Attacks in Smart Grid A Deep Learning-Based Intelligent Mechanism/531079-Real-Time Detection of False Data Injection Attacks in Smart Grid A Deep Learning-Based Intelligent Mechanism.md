# Real-Time Detection of False Data Injection Attacks in Smart Grid: A Deep Learning-Based Intelligent Mechanism

## 笔记作者
Sakura

## 基本信息

* 标题
  
  Real-Time Detection of False Data Injection Attacks in Smart Grid: A Deep Learning-Based Intelligent Mechanism
  
* 作者

  Youbiao He, Student Member, IEEE, Gihan J. Mendis, Student Member, IEEE, and Jin Wei, Member, IEEE

* 刊物出处：

  IEEE Transactions on Smart Grid ( Volume: 8 , Issue: 5 , Sept. 2017 )

* 链接：
  
  https://sci-hub.ren/10.1109/tsg.2017.2703842




## 主要内容

  本文提出了一种基于深度学习的FDI攻击实时检测方案。通过建立优化模型，提出了一种以电力盗窃为目的的FDI攻击。本文提出的方案利用条件深度信念网络(CDBN)，有效揭示了避开SVE机制的不可观测FDI攻击的高维时间行为特征，利用捕获的行为特征来实时检测潜在的FDI攻击。本文通过IEEE 118总线测试系统的仿真，验证了该策略的有效性，还使用ieee300总线测试系统评估了所提出的检测机制的可扩展性。本文所提出的检测机制有效地放宽了对潜在攻击场景的假设，并实现了较高精度。


## Mechanism & Structure

![JhPuuV.png](https://s1.ax1x.com/2020/04/27/JhPuuV.png)
![JhP1N4.png](https://s1.ax1x.com/2020/04/27/JhP1N4.png)

## 创新点

* 有效放宽了对潜在攻击场景的假设
* 在放宽攻击场景的假设下实现了较高精度
* 创新的在条件深度信念网络CDNB的基础上，揭示了不可观测到的FDI攻击的高维时间行为特征
* 设计出一种优化模型来描述偷取电力的FDI攻击，假设攻击者使用这种攻击方式，然后用本文提出的CDBN模型去检测
* 利用深度置信网络CDBN对大规模历史数据进行训练，通过仅对模型网络中的第一个隐藏层进行CGBRBM技术，而对于其他隐藏层均使用常规的RBM技术，减少了训练时间和复杂度

## 不足之处

* 本文假设FDI攻击只能破坏有限数量的负载配置文件。但是实际场景中由于攻击者资源可能多于本文所假定的资源，故检测效果在实际应用情况中可能下降
* 本文共分为4种情况进行模拟，但是各个例子中所考虑的因素太少，不够全面。例如只评估了三个因素对检测精度的影响、偶尔存在操作故障而导致状态测量结果出现偏差等
* 本文只检测了提出的一种电力偷窃攻击，不能实现检测FDI攻击手段的多样性

## 改进方法
1. 对每种情况进行模拟时增加其影响因素
2. 可以采取多种神经网络结构在每种情况下进行性能对比，避免只在case 1中比较不同检测方案而其他3个cases中都缺少此内容
3. 对于FDI攻击可能破坏的负载配置文件数量，可考虑对实际情况进行调研后进行假定，增加其真实性。或采取在不同被破坏的负载配置文件数量下给出检测机制的性能对比以证明其鲁棒性
4. 增加模拟时的电网系统种类，如IEEE 69总线系统，IEEE 14总线系统等，避免对检测机制扩展性实验出现样例不足问题
5. 增加FDI攻击手段，避免FDI攻击过于单一

