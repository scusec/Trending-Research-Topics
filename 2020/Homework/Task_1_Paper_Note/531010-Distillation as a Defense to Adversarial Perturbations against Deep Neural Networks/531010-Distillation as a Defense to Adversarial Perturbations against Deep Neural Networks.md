# Distillation as a Defense to Adversarial Perturbations against Deep Neural Networks
## 基本信息
> 出处 : 37th IEEE Symposium on Security & Privacy, IEEE 2016. San Jose, CA.

> 作者 : Nicolas Papernot
, Patrick McDaniel
, Xi Wu
, Somesh Jha
, and Ananthram Swami

> 机构 : Department of Computer Science and Engineering, Penn State University
§Computer Sciences Department, University of Wisconsin-Madison
United States Army Research Laboratory, Adelphi, Maryland

## 摘要
深度学习在传统机器学习领域的各类问题表现都很突出，但是其存在一个问题，就是容易受到对抗性样本的攻击。通过输入一个被特殊构造过的样本，误导深度学习做出错误判断，有心的攻击者在未来可能用这个漏洞造成智能车事故。这篇文章探讨了一种基于蒸馏网络的防御方式，据说可抵抗大部分对抗性样本攻击。


## 主要内容
### 概念
1. 知识蒸馏
知识蒸馏的概念提出应该是这篇2015年文章中来的[Distilling the Knowledge in a Neural Network](https://arxiv.org/abs/1503.02531)。最近则是因为大型模型如Bert、GPT较为笨重，为解决线上部署的运行时间问题而被不断提起。其主要目的是进行知识压缩，将多个模型的知识压缩到一个模型上(大架构到小架构)，实现迁移。该模式下，通常称训练好的模型为teacher模型，进行训练的模型成为student，训练任务在于使得同一输入下，student网络的输出与teacher网络的输出趋近。<br>
而本文中的teacher网络和student结构如下
![YF8rLQ.png](https://s1.ax1x.com/2020/05/05/YF8rLQ.png)

2. 软硬标签
* 硬标签--非0即1
* 软标签--网络输出的标签，表现为概率分布


3. 文章中使用的DNN架构
文章假设的是白盒攻击，即DNN的结构对攻击者公开的情况。DNN结构如下。
![YF8con.png](https://s1.ax1x.com/2020/05/05/YF8con.png)<br>
比较值得注意的是，由于蒸馏网络是为了学习teacher网络的知识，而如果一个DNN训练得十分优良，其输出分布会极其不均衡，以图形识别为例，识别为苹果的概率极高，其余近似为零，这将导致新模型无法获得苹果与桃子相似这一知识。因此蒸馏网络通常会使用特殊的softmax函数。
![YF8wz8.png](https://s1.ax1x.com/2020/05/05/YF8wz8.png)
* N代表输出层维度
* Zi代表原始输出层(最后的隐藏层)输出分量
* T是蒸馏网络内的参数，一般叫做蒸馏温度。

4. 对抗性样本的生成
对抗性攻击主要是通过在样本上加入扰动完成的。原本的模型训练时趋向于损失函数减小，而对抗性攻击反其道而行之，其通过加扰动改变损失函数趋向性(比如non-targeted攻击是往损失函数增大的方向跑)。这篇文章也提到了一般性的对抗样本生成方法。
![YF8yZj.png](https://s1.ax1x.com/2020/05/05/YF8yZj.png)<br>


### 思路和算法
1. 样本生成
* 方向敏感度估计
计算其各个分量的正向导数，称为Fi如下
![YF86ds.png](https://s1.ax1x.com/2020/05/05/YF86ds.png)
* 添加扰动
根据第一步的Fi，可以知道各个方向上的敏感性，自行选择敏感度较高的方向添加扰动，这样可以使得对原图像扰动最小的情况下，干扰效果最好。


2. 防御蒸馏
作者在这部分提出为什么防御蒸馏是有效的。
* 关于分类的知识不仅仅在模型参数中，也在模型输出的概率中。
* 平滑模型的敏感度。前面的样本生成里，计算出的敏感度较大意味着微小的扰动就可以达到攻击目的。通过控制蒸馏中的T参数，可以使得敏感度在各方向分布较为相近，T无限增大则趋近于均匀分布。

3. 具体算法
* 原始数据集 X 和 Y去训练DNN
* 从DNN中获得概率分布F(X)
* X与F(X)输入到架构与蒸馏温度都相同的student网络
* 利用新的网络进行预测。
![YF8rLQ.png](https://s1.ax1x.com/2020/05/05/YF8rLQ.png)


### 实验
以MINST和CIFAR作为实验。
1. 对抗攻击成功率
随着温度T的升高，对抗攻击的成功率下降。
![YF8BQS.png](https://s1.ax1x.com/2020/05/05/YF8BQS.png)

2. 模型自身准确率
准确率有一定下降，但不会很低。
![YF8dRf.png](https://s1.ax1x.com/2020/05/05/YF8dRf.png)

## 创新点
1. 首个使用蒸馏网络防御对抗性攻击的。
2. 平滑分类趋势的思想很有趣。

## 不足之处
1. 维度变高的时候，我觉得正确分类的概率特别高，其余分类的概率将极大趋向于0，蒸馏网络难以学习到对应知识。分类的平滑很难做到。
2. 若已知预测模型F使用了蒸馏网络，那么可以针对蒸馏网络做对抗性攻击。
3. 其实可以直接对数据本身进行图形学的过滤处理，效果也很好。蒸馏网络的训练工作量较大，且会有精确度的部分损失。