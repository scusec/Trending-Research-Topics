## BAT: Deep Learning Methods on Network Intrusion Detection Using NSL-KDD Dataset
#### from: https://dblp.uni-trier.de/db/journals/ejisec/ EURASIP Journal on Information Security(Springer)
#### 论文连接🔗https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8988230（CCF推荐期刊）
#### 论文作者：TONGTONG SU , HUAZHI SUN, JINQI ZHU , SHENG WANG, AND YABO LI
#### 论文笔记：SongJiarui  2017141531023
### 摘要：
针对现有的常用入侵检测方法KNN，SVM等准确率低的缺点，这篇论文提出了用BAT的模型改进，双向长短时记忆网络和注意力机制，注意力机制用双向LSTM后的网络流向量，这些向量包含了重要的特征向量。另外还引用了多层卷积处理数据。此论文提出的端到端的模型，不使用特征工程，用深度学习的自学习层次结构选出关键的特征。在公开的数据集上进行实验，并且对比了其他的模型效果。有一个很重要的贡献点是：它可以很好地描述网络流量行为，提高了网络流量的描述能力有效地检测异常。
### 其他已有的入侵检测工作：
* RNN将网络数据流当作序列模型，RNN中的LSTM可以将所有的攻击类型都用于训练。
* NN将网络数据流变成2维的图片，将数据流之间视为独立的个体，每张“图片”之间没有关联。
* 本文提出的：先前的工作没有涉及到网络数据的结构和格式。使用BLSTM学习每一个数据包的特征，得到一个相关联的向量。注意力机制在序列的数据基础上获得更好的特征集合，这一特征选择的过程没有使用传统的特征工程算法，最后用全连接层和softmax分类器来输出。在NSL-KDD这个数据集上BAT-MC这个模型的准确率达到84.25% ，比CNN和RNN模型分别高出了4.12% 和2.96%
### 这篇论文的贡献：
- [x] 提出端到端的深度学习模型BAT-MC（BLSTM+attention+Multiple Converlution layers）
- [x] 提出注意力机制和BLSTM来做特征选择
- [x] 对比BAT-MC模型和传统的CNN和RNN，很好的利用了网络数据流的结构特征，能够很好的捕捉有用特征
- [x] 在NSL-KDD上实验，BAT-MC比传统的模型准确率高
![image.png](https://i.loli.net/2020/03/15/xuC9WvbOIZA4jNM.png)
### 模型的训练
模型的训练包括前向传播和方向传播。前向传播主要是BLSTM和attention层，它们分别代表不同的结构，因此扮演着不同的角色。NSL-KDD被分为了训练集合和测试集，数据集在one-hot和正则化以后，传入BAT-MC模型。
![image.png](https://i.loli.net/2020/03/15/3W1oFvbDKaiSTfA.png)
![](https://pic.downk.cc/item/5e6dbf0be83c3a1e3ac53777.png)

![](https://pic.downk.cc/item/5e6dbe97e83c3a1e3ac4ec70.png)

实验分别做了2分类和多分类的攻击检测
![](https://pic.downk.cc/item/5e6dbef5e83c3a1e3ac5277d.png)
![](https://pic.downk.cc/item/5e6dbf25e83c3a1e3ac549b5.png)

### 对比实验
![](https://pic.downk.cc/item/5e6dbf7ee83c3a1e3ac5894d.png)

![](https://pic.downk.cc/item/5e6dbf8fe83c3a1e3ac5957c.png)

### 结论
现有的传统深度学习模型没有很好的利用入侵检测的数据特征，时间序列的特征可以让BLSTM像处理自然语言一样处理网络数据流，注意力机制也很好的发挥了优势，有别于特征工程选出了很好的特征集合。本文主要是用BAT-MC模型在KDDTest+ 和KDDTest-21上进行测试，在NSL-KDD上进行训练，结果表明，有很高的准确率。为入侵检测的做出了一些贡献。
### 我思考的缺点：
BLSTM的收敛慢，时间代价大于传统的深度学习模型，文章没有很好的说明为什么使用深度学习模型选择的特征比其他模型好，没有很好的说服力，单从结果来看确实是准确率提高，但和特征工程PCA、DecisionTree、SelectKbest、Logistics等方法选取特征的优越性，没有进行比较，单是用模型的不同来做实验感觉没有很好的说服在选取特征这一方面有贡献度。