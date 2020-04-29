# Seeing is Not Believing    


* 笔记作者: 江钰坤    

* 原文作者: Qixue Xiao,Yufei Chen,Chao Shen,Yu Chen,Kang Li    

* 原文题目: Seeing is Not Believing: Camouflage Attacks on Image Scaling Algorithms    

* 原文来源: 28th USENIX Security Symposium (2019)    

<h3>因为大多数深度学习计算机视觉应用程序都使用预训练的卷积神经网络（CNN）模型，该模型以由这些模型的输入层定义的固定大小来获取数据。因此，对于用户输入的不同像素数据，需要经过图像缩放算法使其满足输入要求。图像缩放是指在保留图像的视觉特征的同时对数字图像进行调整大小的操作。缩放图像时，缩小（或放大）过程会生成一个像素数比原始像素少（或大）的新图像。在本文中，演示了针对常见缩放算法的自动攻击，即自动生成伪装图像，其伪装图像的视觉语义在缩放后发生了巨大变化。</h3>    

## 1、研究内容    

### 攻击生成机制：攻击图片生成的机制如下图所示，主要分为几个核心部分。    
- srcImg：原始的良性图片  
- targetImg：希望机器识别出来的图片  
- attackImg：生成的提交给服务端的希望被识别的攻击图片
- outImg：经过服务端的缩放功能后，作为缩放功能的输出图片，同样作为神经网络模型的输入图片  
<img src="https://pic.downk.cc/item/5e7ec129504f4bcb04107867.jpg" width="60%" >  
<h4>以上攻击过程可简化为一组方程，CL<sub>m'＊m</sub>和CR<sub>n＊n'</sub>分别是左右系数矩阵，它决定了outImg的尺寸，Δ<sub>1</sub>被定义为扰动矩阵。</h4>
<img src="https://pic.downk.cc/item/5e7ec4b0504f4bcb0413134a.jpg" width="60%" >  
<h4>对于开放的神经网络模型，它的outImg尺寸是可知的，但是对于黑盒模型，需要反向运算求出其尺寸。作者使用下图所示的简化算法，使用近似运算牺牲很小的精度求出了需要的数据.</h4> 
<img src="https://pic.downk.cc/item/5e7ecaa7504f4bcb04179272.jpg" width="60%" >  
<h4>对于扰动矩阵Δ<sub>1</sub>的生成作者在进行维度拆分化简后使用了凹凸编程方法，文中未做过多赘述</h4>  

### 实验数据：攻击实验所用图片如下图所示。
<img src="https://pic.downk.cc/item/5e7ecd08504f4bcb04195f9e.jpg" width="80%" >  

### 实验结果：该攻击主要针对Microsoft Azure, Baidu,Aliyun和Tencent cloud vision services所展开，基本都很好地实现了攻击的需求，并且攻击结果判断得到了较高的置信度，得到的攻击结果如下图所示。
![](https://pic.downk.cc/item/5e7ece40504f4bcb041a210d.jpg)  

## 2、创新点  
### 本文主要有如下创新点：  
1. 优化算法，在计算中多次将矩阵运算拆分成向量运算，或在牺牲少量精度的情况下大幅提升运算效率。
2. 对于黑盒攻击，因为无法直接获取其包含的缩放尺寸，作者构建了一个特殊的标志图片（如下图所示），在缩放至不同的尺寸后，图片被识别为不同属性。  
<img src="https://pic.downk.cc/item/5e803296504f4bcb040c4812.jpg" width="80%">  
3. 在对神经网络模型判断产生了有效的攻击结果之后，作者还发掘了一种针对人类视觉效果的攻击，即因为用户使用不同的浏览器而对于同一图片获取到了不同视觉效果。（如下图所示）  
<img src="https://pic.downk.cc/item/5e8035f6504f4bcb040e9a26.jpg" width="80%">
4. 提出了两种有效的攻击检测机制，分别是基于颜色直方图的检测和基于颜色散射的检测，都获得了较好的检测效果。（如下图所示）  
<img src="https://pic.downk.cc/item/5e803946504f4bcb04110648.jpg" width="80%">  

## 3、目前缺陷  
### 本文主要存在以下缺陷
1. 在针对主流白盒模型的攻击之中，部分模型攻击效果欠佳，（如下图所示）作者将原因归结于其算法过于复杂或者过于冷门，并未对其进行分类分析，我认为还可以再进一步展开分析。  
<img src="https://pic.downk.cc/item/5e8039fd504f4bcb04118b9a.jpg" width="80%">  
2. 对于浏览器的视觉干扰无法实现针对攻击，可以对不同浏览器使用的缩放算法提取唯一特征，进而实现针对攻击。
