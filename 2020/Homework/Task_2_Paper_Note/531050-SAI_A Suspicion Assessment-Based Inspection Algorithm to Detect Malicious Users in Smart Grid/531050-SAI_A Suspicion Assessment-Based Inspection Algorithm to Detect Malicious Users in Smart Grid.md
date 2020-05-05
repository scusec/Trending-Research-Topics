# SAI: A Suspicion Assessment-Based Inspection Algorithm to Detect Malicious Users in Smart Grid 

## 1、论文主要内容总结
<h3>智能电网相较传统电力系统有许多优势，但先进设备与系统的应用同样给智能电网带来了受攻击的风险。除此之外，因为攻击成本低等因素，现有的检测手段面临了准确率低、成本高的问题。针对这一问题，作者提出了一个基于怀疑的检测算法（SAI），算法重点关注用户的过往诚信记录与各阶段的电力消耗偏差值，得出不同用户的怀疑值构建出用于检测的二叉树。实验结果表明，该算法优于现有其他方法。</h3>


## 2、论文基本信息

* 原文题目: SAI: A Suspicion Assessment-Based Inspection Algorithm to Detect Malicious Users in Smart Grid  
* 原文作者: Xiaofang Xia ,Yang Xiao , Senior Member, IEEE, and Wei Liang , Senior Member, IEEE
* 原文来源: IEEE TRANSACTIONS ON INFORMATION FORENSICS AND SECURITY, VOL. 15, 2020  
* 链接：https://ieeexplore.ieee.org/document/8731931  
* 笔记作者: 江钰坤 
 

## 3、论文主要创新点    
### 我认为本文在构建检测算法时，综合了横向与纵向对比，构建了很好的模型
* 对于同一用户，引入犯罪学的调查，基于累犯概率的分析（如图-1）针对用户过往记录赋予不同的置信度
  ![](https://pic.downk.cc/item/5e91c458504f4bcb04d95a3b.jpg)
  <p align="center">图1</p>
* 对于具有相同预测性质的不同用户，对比其检测数据的差异（如图-2）来分析异常
  ![](https://pic.downk.cc/item/5e91c47b504f4bcb04d97c04.jpg)
  <p align="center">图2</p>
* 单独检测与二叉树算法结合（如图-3），进而实现了算法复杂度与精度之间的权衡
  ![](https://pic.downk.cc/item/5e91c49d504f4bcb04d99fe4.jpg)
  <p align="center">图3</p>


## 4、论文的缺点

1. 在对有犯罪记录（窃电）用户进行累犯率r(i,t)进行归一化时，作者选用的是Sigmoid函数（如图-4）。但可以在前文的数据（如图-1）中得知，犯罪记录信息是离散的，Sigmoid函数并非最佳选择
   ![](https://pic.downk.cc/item/5e91c3d3504f4bcb04d8d8b2.jpg)
   <p align="center">图4</p>

2. 在对用户可能的犯罪率s(i,t)进行评估时，作者考虑到了随着观测时间增长，偏离风险h(i,t)（即该时间内用户的电量消耗实际观测值与预测值相差巨大）所占的权重应不断上升，因此得出如图-5所示的公式。但是，我认为(1-μ)该变量并不适合
   ![](https://pic.downk.cc/item/5e91baa7504f4bcb04cf13b1.jpg)
  <p align="center">图5</p>
   

## 5、可能的改进方法
1. 针对缺点1，我认为在对有犯罪记录的用户的累犯率r(i,t)进行归一化处理时，考虑到数据是离散数据，我认为可以提出两点适合的解决方案。
   * 使用Softmax函数进行拟合。Softmax函数多用于离散数据的多分类问题，因为犯罪数量>0，所以需要在使用时对函数进行一个整体向右的平移与翻转操作，再进行一个阈值截断，其拟合值有一定概率比Sigmoid更能反映真实情况。
   * 使用机器学习算法训练拟合函数。理想的函数模型往往无法拟合真实的场景，如果具有一定量的数据规模，完全可以训练得出一个相对更加成熟的机器学习模型来生成参数。

2. 针对缺点2，我们从图2可以得知，偏离风险h(i,t)的准确率与采样时间长短并非(1-μ)类型的线性关系，一个区间内的面积之差只至少应该使用二阶以上的函数进行拟合，根据文章所提供的函数图形进行分析，个人认为可以使用以某一正态分布为导数的函数作为其权重函数模型。


