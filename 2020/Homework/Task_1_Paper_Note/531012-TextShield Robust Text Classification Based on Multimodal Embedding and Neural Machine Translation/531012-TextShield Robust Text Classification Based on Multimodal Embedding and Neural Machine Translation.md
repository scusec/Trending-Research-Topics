# 论文信息

标题：TextShield: Robust Text Classification Based on Multimodal Embedding and Neural Machine Translation [[PDF](https://nesa.zju.edu.cn/download/TEXTSHIELD%20Robust%20Text%20Classification%20Based%20on%20Multimodal%20Embedding%20and%20Neural%20Machine%20Translation.pdf)]

作者：Jinfeng Li, Tianyu Du, Shouling Ji, Rong Zhang, Quan Lu, Min Yang, Ting Wang

出处： USENIX Security 2020

链接：https://www.usenix.org/system/files/sec20fall_li-jinfeng_prepub.pdf

笔记作者：Fr3ya

# 主要工作
在一些社交平台中，为了避免监管，会对原始的恶意的文本内容经过处理，比如用其他字符代替，中间加符号等方式来避免被检测到，日常的基于深度学习的文本分类容易收到恶意制作的对抗性文本的攻击。在这篇论文中，提出了一种针对中文的对抗防御框架，可对这些对抗性文本进行检测。

## contribution
- 提出了一种多模态的嵌入方案，来增强DLTC模型的鲁棒性，首次将对抗性NMT应用于重建原始文本。
- TEXTSHIElD对恶意用户生成的混淆文本具有较高的准确性，与良性输入相比，对模型性能的影响很小。

# 框架设计
## Framework
这一个框架基于多模态嵌入、多模态融合和NMT构建。框架图如下图所示：

![p1][1]

步骤分为以下几个步骤
1. 将文本内容输入到经过大量的对抗-良性文本对训练的NMT模型中。
2. 将校正的文本输入到DLTC模型中，以用来多模态嵌入从语义、字形、发音级别来提取特征。
3. 最后将提取的特征融合到常规分类中。
## 对抗翻译
提出了**基于神经网络机器翻译的对抗校正器**，框架图如下图：


![p2][2]

这一部分比较好理解，就是一个普通的seq2seq Attention模型，将句子中的每一个字嵌入，得到一个输入序列，然后经过一个编码器，得到一个固定长度的序列，然后解码器再将这个序列进行解码，得到和输入序列长度一样的一个序列，就是seq2seq，这种方式也常用于文本纠错中。

## 模型训练
首先通过对抗攻击生成大量的句子对，然后训练设计的NMT模型。为了避免误差在训练过程中被逐步放大，让它快速收敛，就使用了teacher forcing技术(在训练时，使用前$T-1$个step的ground truth来输出第T个step的值)

## 对抗纠正
训练完成后，NMT模型将用作对抗性文本校正器，以通过翻译重建原始文本。为了提高NMT模型的表现，在解码阶段采用了beam-search来搜索最优的翻译

## 多模态嵌入
为了绕过审查，常用的就是在字形和发音上的干扰。
### 语义嵌入
使用`skim-gram`模型来学习连续的语义词向量(将重点放在了字符级的嵌入上，因为单词级嵌入受语音的影响最大)。
### 字形嵌入
中文里面大量的字符看起来一样但是却是不同的意思，所以就需要从形态方面来提取字形特征。将字形转换为一个图像，然后利用卷积神经网络提取字形特征向量。
### 字音嵌入
设计了一种语音嵌入的方法，用汉语拼音进行标注，保留文本中的非汉字，最后获得一个包含N个拼音形式的新的序列，最后将每个字符的拼音形式嵌入到skip-gram模型。针对一些突变的单词。比如“涩情”和“色情”

## 两种多模态的融合方式

![p3][3]

# 实验设计
主要使用TextCNN和BILSTM实现
## 攻击方法
对于词汇的攻击方式，主要分为以下几种类型：

![p4][4]

## 评估方式
### 翻译评估
- 字错误率
- BLEU
 一种均匀加权的方式，为了平衡各统计量的作用
- 语义相似度
### 稳健型评估
- 攻击成功率
- 困扰的词
- 查询
### 效用评估
- Edit Distance
- Jaccard Coefficient

![p5][5]

![p6][6]

![p7][7]

![8][8]

#目前不足
1. 在本文中作者考虑了6种攻击方式，但是实际的攻击的逃避方式可能会更多，比如说`智障->zhi zhang->zhi zh@ng` 这种扩展下的情况没有考虑到，实际上这种也是很普遍的一种情况，而且多种攻击方式相混合的方式也很常见。
2. 本文实现了比较好的效果，但是时间代价会比较高，需要降低成本， 可以使用模型压缩技术或者分布式计算的技术。
3. 对于字音、字形方面的逃逸，可以采用使用特定术语，从而导致检测到更加困难。



[1]: https://pic.downk.cc/item/5eaf7c28c2a9a83be54f3971.png
[2]: https://pic.downk.cc/item/5eaf7c3bc2a9a83be54f498a.png
[3]: https://pic.downk.cc/item/5eaf7c4ac2a9a83be54f58f8.png
[4]: https://pic.downk.cc/item/5eaf7c5ec2a9a83be54f6e9a.png
[5]: https://pic.downk.cc/item/5eaf7c77c2a9a83be54f8860.png
[6]: https://pic.downk.cc/item/5eaf7c86c2a9a83be54f96f5.png
[7]: https://pic.downk.cc/item/5eaf7c77c2a9a83be54f8860.png
[8]: https://pic.downk.cc/item/5eaf7cacc2a9a83be54fbc87.png