# Devil in the Detail: Attack Scenarios in Industrial Applications

*注：由于我在给出的顶会和期刊链接里找了比较久时间却没有找到关于智能电网的相关文章，所以选择了一篇相接近的工业控制相关的会议论文，希望老师能够理解通融*

## Message of Paper

* **title**：
  Devil in the Detail: Attack Scenarios in Industrial Applications

* **writers**：

  * 1 st Simon D. Duque Anton
    Intelligent Networks Research Group
    German Research Center for AI
    67663 Kaiserslautern, Germany
    Simon.Duque_Anton@dfki.de
  * 2 nd Alexander Hafner
    Intelligent Networks Research Group
    German Research Center for AI
    67663 Kaiserslautern, Germany
    Alexander.Hafner@dfki.de
  * 3 rd Hans Dieter Schotten
    Intelligent Networks Research Group
    German Research Center for AI
    67663 Kaiserslautern, Germany
    Hans Dieter.Schotten@dfki.de

* **from&site**：

  Devil in the Detail: Attack Scenarios in Industrial Applications.
  2019 IEEE Security and Privacy Workshops (SPW).

  https://sci-hub.tw/10.1109/spw.2019.00040

## Paper Framework

* **works**：
  *  an overview of possible attacks for industrial networks is provided.
    一个概述包括了所有的可能的工业控制系统网络攻击
  *  Attack vectors are analysed and categorised, with an emphasis on industrial network protocols
    攻击向量根据工控系统的协议被分析和分类
  * the simulation of a real-world scenario is presented, as well as attacks on this scenario
    **two machine learning-based methods for time series anomaly detection are employed to detect the attacks.** （有两种机器学习模型被提出去检测这种攻击）
* **background**： 
  * For decades, the industrial domain has been deemed secure due to two reasons: First, the physical separation of networks. Second, each network was created in an application specific fashion, rendering it extremely difficult for an attacker to exploit it.
    **前些年工业领域被认为是安全的因为是使用物理的网络，而且每个网络都是用于特定的应用从而很难被攻击者利用**
  * While industrial networks have been unique in their applications specific nature, the establishment of Commercial Off The Shelf (COTS) hard- and software introduces standardised modules. This makes set up and maintenance much easier, but also drastically increases the effect of vulnerabilities in one of the modules
    **可软编程的硬件（嵌入式系统）的使用导致可能出现各种各样的漏洞**
  *  A deep understanding of these characteristics is required in order to effectively protect industrial networks.
    **传统的网络安全设备难以适用于工业控制系统的网络中去，所以更加需要一种深层次的符合工控网络特点的有效率的安全保障设备**

## Process

* **INDUSTRIAL ATTACKS（工控攻击介绍）**

  *  The first step in attacking industrial environments is commonly the breach of the perimeter.（第一步通常是突破边界）
  * After breaking the perimeter, the ICS or the field devices respectively have to be taken over.（然后是接管集成电路或现场设备）
  * Some malware could stay undetected for long periods of time, at least partly due to missing or insufficient security procedures for industrial networks.
  *  The difficulty of industrial malware lies in the profound knowledge the malware authors needs to have about the targeted systems. （难点在于攻击者需要对目标系统足够了解）

* **PROCESS ENVIRONMENT AND ATTACK SCENARIOS**

  * The process this work is based upon has been used to generate data for industrial intrusion detection already. It is shown in Figure 1.

    ![pic1](https://pic.downk.cc/item/5ea2e30cc2a9a83be5ba4fb9.png)

    图中包括两个水容器，水是用泵P101泵送，由直流电动机M101驱动从容器1到容器2，直到达到阈值。这个用不同的传感器S111和S112测量水位，以及电容式传感器B113和B114。此外，A测量容器间液体流量的叶片传感器1和容器2，B102和一个PT100温度传感器，使用B104。释放容器2的水，一个螺线管使用M102阀门。这种行为的典范流程在图2中显示为一个时间序列。精选过程参数，所有这些都是传感器输出显示正常操作。此操作已执行关于场景的实际实现创建此工作中分析的模拟。为了这项工作，上述环境已扩展到5个实例。它们是用真实的硬件来模拟的。

  * Two scenarios have been implemented and evaluated in this work.（在这项工作中，已经实现并评估了两个场景。）

* **EVALUATION**

  * 检测所讨论攻击的方法通过数据集上显示和评估。作为输入值进入异常检测。它们很容易扩展，但被证明是最具解释性的变量。

## Conclusion

* 在这项工作中，我们讨论了工业环境中的攻击场景。从这些场景中，派生并实现了一个用例。之后，攻击场景引入到场景中。采用两种基于时间序列的异常检测方法对攻击进行检测。矩阵剖面的性能令人满意，易于检测攻击。只有一个鲁棒的超参数和无监督的训练，使得应用领域之间的使用和传输变得容易。LSTM方法不能很好地工作，它预测了攻击行为和正常行为。这种结果可能源于过拟合，因为规则的时间序列让神经网络学习某些倾向，却不会泛化。
* 上下文信息或基于机器学习的分类方法也可以解决这个问题。

## Consider about

* 在不同系统的设计之间如何时机器学习模型得到一个泛化的训练过程，这一点还没有很好的被解决
* 同时工控系统具和普通计算机网络相比有较高的复杂性，能否将这些复杂性的来源进行划分，然后使用不同的模型进行考虑也是一个值得思考的点