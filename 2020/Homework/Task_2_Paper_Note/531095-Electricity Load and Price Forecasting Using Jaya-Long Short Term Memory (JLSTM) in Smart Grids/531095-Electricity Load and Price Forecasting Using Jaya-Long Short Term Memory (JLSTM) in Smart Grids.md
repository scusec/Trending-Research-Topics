### 论文阅读笔记

#### 论文题目：Electricity Load and Price Forecasting Using Jaya-Long Short Term Memory (JLSTM) in Smart Grids

#### 论文作者：Rabiya Khalid, Nadeem Javaid, Fahad A. Al-zahrani, Khursheed Aurangzeb, Emad-ul-Haq Qazi and Tehreem Ashfaq

#### **论文出处：https://www.mdpi.com/1099-4300/22/1/10**

#### **论文主要内容：**

​		这篇论文通过RNN、LSTM等方法，利用大数据对电价和需求进行预测。作者提出了一种多变量预测模型jaya-LSTM，利用jaya优化算法对超参数进行调整，通过均方根误差(RMSE)和平均绝对误差(MAE)进行进度预测。本文的创新性在于结合了循环神经网络RNN和长短期记忆网络LSTM，并在数据预处理时删除了缺失值和异常值，提高了预测精度。

#### 可能存在的缺陷：

​		训练 RNN 和 LSTM 都比较困难，因为计算能力受到内存和带宽等的约束。如果要快速训练RNN，需要消耗大量计算资源；LSTM可以绕过一些单元，对长时间的步骤进行记忆，一定程度上补救了梯度消失的现象，但从前面单元传来的序列路径依然存在，随着网络的加深会变得越来越复杂。

​		

