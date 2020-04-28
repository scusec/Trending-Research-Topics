# Neural Cleanse: Identifying and Mitigating Backdoor Attacks in Neural Networks
Backdoor Attacks in Neural Networks

Backdoor Attacks in Neural Networks

## Message of Paper

* **title**：
  Neural Cleanse: Identifying and Mitigating
Backdoor Attacks in Neural Networks
  
* **writers**：

  Bolun Wang ∗† , Yuanshun Yao † , Shawn Shan † , Huiying Li † , Bimal Viswanath ‡ , Haitao Zheng † , Ben Y. Zhao †
  ∗ UC Santa Barbara, † University of Chicago, ‡ Virginia Tech

* **from&site**：

  2019 IEEE Symposium on Security and Privacy, SP 2019, San Francisco, CA, USA, May 19-23, 2019. IEEE 2019, ISBN 978-1-5386-6660-9
  Session 8: Machine Learning

  https://sci-hub.tw/10.1109/sp.2019.00031

## Paper Framework

* **works**：
  present the first robust and generalizable detection and mitigation system for DNN backdoor attacks
  提出了第一个健壮且可概括的检测和DNN后门攻击的缓解系统
* **background**： 
  In the security space, DNNs are used for every-thing from malware classification, to binary reverse-engineering and network intrusion detection
  在安全领域，DNN用于来自恶意软件分类的事情二进制逆向工程和网络入侵检测
* **problem**：
  Without transparency, there is no guarantee that the model
  behaves as expected on untested inputs.This is the context that enables the possibility of backdoors or “Trojans” in deep neural networks. 
  没有透明性或称可解释性，使得神经网络中可能隐藏后门
* **goal**：
  Given a trained DNN model, our goal is to identify if there is an input trigger that would produce misclassified results when added to an input, what that trigger looks like, and how to mitigate, i.e. remove it from the model.
  对于一个给定的深度网络可以去判断是否存在触发器使得某些输入会获得一个错误的分类，并发现该触发器的形式，以及给出减轻和移除的方法

## Trigger put in example

![image-20200419180514858](https://pic.downk.cc/item/5ea2e296c2a9a83be5b994d7.png)

## process

* key intuition of detecting back-doors：
  in an infected model, it requires much smaller modifications to cause misclassification into the target label than into other uninfected labels（通过导致误分类的修改程度来判断）
* Steps：
  1. For a given label, we treat it as a potential target label of a targeted backdoor attack. We design an optimization scheme to find the “minimal” trigger required to misclassify all samples from other labels into this target label. In the vision domain, this trigger defines the smallest collection of pixels and its associated color intensities to cause misclassification.
     对于每一个标签当作可能的触发点，通过设计一种优化方案找到所需的最小的触发点使得分类错误。
  2. repeat Step 1 for each output label in the model.
     For a model with N = |L| labels, this produces N potential
     “triggers”.
     重复上述第一步，计算出所有潜在的触发点的值。
  3. After calculating N potential triggers, we measure the size of each trigger, by the number of pixels each trigger candidate has, i.e. how many pixels the trigger is replacing. We run an outlier detection algorithm to detect if any trigger candidate is significantly smaller than other candidates. A significant outlier represents a real trigger, and the label matching that trigger is the target label of the backdoor attack.
     计算出第二步中的N个可能的触发点后，测量每个触发器的大小，即需要替换多少像素后会产生问分类。然后使用离群值检测相关方法对明显的触发器进行提取。
  4. Step 1 also produces the trigger responsible for the backdoor, which effectively misclassifies samples of other labels into the target label. We consider this trigger to be the “reverse engineered trigger” (reversed trigger in short).
     验证后门触发器
  5. Mitigating Backdoors.
     削弱后门触发器

## Conclusion

* Our work describes and empirically validates our robust and general detection and mitigation tools against backdoor (Trojan) attacks on deep neural networks.
* differences between two backdoor injection methods: the trigger-driven BadNets end-to-end attack with full access to model training, and the neuron-driven Trojan Attack without access to model training.
  两种攻击方式的发生场景不相同，BadNets需要对网络的训练有控制权，而木马攻击注入方法并不需要，而是采用一种注入的方式进行。
* 通过实验，发现木马攻击注入方法通常会增加更多超出必要的摄动，并引入不可预测的改变为非靶向神经元。这些触发器难以进行反向工程，并使它们更具抵抗力过滤和神经元修剪。但是，对特定神经元的专注训练可以使有用的神经元变得极为敏感，所以该种攻击可以通过学习来缓解。
  相反，BadNets引入更容易使预测神经元的变化，并且更容易通过神经元修剪进行逆向工程，达到过滤和缓解的效果。

## Consider about

* 该论文所提出的检测方法在一定层度上是假设时域空间存在一种自然分布，且所有的该机器学习的输入和输出之间都在概率上满足这样的一致关系。所以才会有被隐藏了触发器的类别标签的阈值较低的这种距离测量方式来对触发器进行判断。但该种假设仍需要进一步实验的证明。
* 是否可以从频域的角度对该研究方向进行考察

