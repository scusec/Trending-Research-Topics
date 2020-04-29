# 标题：
##CDN Judo: Breaking the CDN DoS Protection with Itself

# 作者：
##Run Guo, Weizhong Li, Baojun Liu, Shuang Hao, Jia Zhang, Haixin Duan, Kaiwen Shen, Jianjun Chen, Ying Liu
#出处：NDSS 2020

# 链接：
##https://www.ndss-symposium.org/ndss-paper/cdn-judo-breaking-the-cdn-dos-protection-with-itself/

# 论文简要：
交付网络（CDN）通过其全球分布的网络基础设施，提高了网站的访问性能和可用性，促进了CDN驱动的网站在互联网上的蓬勃发展。由于CDN驱动的网站通常运行重要的业务或关键服务，攻击者最感兴趣的是摧毁这些高价值的网站，以达到最大影响的严重损害。由于CDN以其巨大的带宽资源吸收了分布式攻击流量，人们普遍认为CDN供应商为CDN驱动的网站提供了有效的DoS保护。然而，我们发现CDN的转发机制中的实现或协议缺陷可以被利用来破坏这种CDN保护。在本研究中，我们特别提出三种CDN威胁以及讨论了可能的缓解措施。

#主要内容：
本文通过对6个CDN转发行为的实证研究，揭示了CDN本身可能被滥用来攻击CDN背后的源（网站服务器）。主要通过向CDN发送精心编制但合法的请求，攻击者可以对源发起DoS攻击，从而破坏CDN DoS保护，有以下三种威胁：
1. HTTP/2 Bandwidth Ampliﬁcation Attack：因为CDN在客户端-CDN连接中仅支持HTTP/2，因此攻击者可以滥用CDN的HTTP/2-HTTP/1.1转换行为，对源服务器发起带宽放大攻击（解决方案：分析了引入HTTP/2的HPACK压缩机制，发现HTTP/2的并发流和Huffman编码可能被滥用，从而进一步提高带宽放大系数。）
2. Pre-POST Slow HTTP Attack：在本研究中分析的六个CDN中有三个在接收到POST头时就开始转发httppost请求，而不是等待整个POST消息体。此预发布行为可能会被滥用以耗尽源站的连接限制，并使其他合法用户请求匮乏，从而导致对源站的缓慢HTTP DoS攻击。更糟糕的是，这些CDN的HTTP/1.1后转发和HTTP/2后转发行为都易受此威胁。
3. Degradation-of-Global-Availability Attack：通过向每个CDN的全局代理IP（入口IP）发送请求以模拟全局客户端访问，我们对每个CDN的业务转发IP（出口IP）的分布进行了大规模测量。结果表明，CDNs将分配一小组出口IP来访问源站，呈现较低的IP流失率。因此，攻击者可以利用此特征，仅通过切断一个或一小组CDN源连接来有效地降低CDN驱动的网站的可用性，从而阻止大多数全球客户端访问网站的服务。例如，对于Max CDN，如果仅断开一个CDN-origin连接，超过90%的全局访问将停止从CDN后面的origin获取资源。
在文章的最后还分析了这些攻击产生的原因以及缓解措施，其中部分是市场竞争。另外的原因具体分析如下：
1. HTTP/2带宽放大攻击：威胁来自CDNs对HTTP/2的半成品支持。（基本上，HTTP/2规范在HTTP/1.1-and-HTTP/2共存环境中缺乏足够的安全考虑。同时，当CDN供应商急于支持HTTP/2以获得以效率为中心的功能时，这些CDN供应商仅在客户机-CDN连接中支持HTTP/2，导致相关规范中没有明确定义HTTP/2-HTTP/1.1转换环境。）缓解措施：CDN厂商应该保守地支持这个新的protocolandmakeitasan“opt-in”optioninstad，而且，如果打开HTTP/2，CDN厂商还应该进一步限制转换后的CDN-origin TTP/1.1连接。
2. 后置慢速HTTP攻击：一般来说，CDN将传统的客户端-网站连接分离为客户端-CDN和CDN-源连接，这是一种自然防御客户端缓慢HTTP攻击的设置。然而，一些CDN的后转发行为使得攻击者能够控制后端CDN源连接。后发威胁利用CDN厂商的意图加速后发，同时引入新的攻击向量。缓解措施：第一让网站管理员在源端实现超时，然而这种解决方法需要在everyCDN供电的网站上进行配置。第二建议CDN供应商实施更严格的后转发机制，如存储后转发
3. 全局可用性攻击降级：CDN的出口IP分配策略具体取决于实现。根据测量，一些CDN供应商的出口IP分配策略是可预测的。缓解措施：切断或阻止较少的CDN源连接，建议CDN供应商调整其出口IP分配策略，使其更加不可预测，例如分配更多出口IP并频繁地搅动它们。

#框图结构：
通过对每种攻击分别进行Attack Surface Analysis, Real-World Attack Analysis（其中第三种攻击多了一个相关进出IP地址的确定）
在Attack Surface Analysis中先分析所面向的对象以及运用到的技术，如对于HTTP/2 Bandwidth Ampliﬁcation Attack则分析HTTP/2的功能与目前存在的问题，Pre-POST Slow HTTP Attack则分析Primer on Slow HTTP DoS Attack技术，然后再分析攻击原则，即上面主要内容中的攻击原理、过程。
Real-World Attack Analysis则是处理自本研究中真实模拟攻击中的数据。
最后总结，得出以上三种攻击是如何利用协议中的缺陷完成对CDN进行的Dos保护的何种损害。

#创新点：
能针对目前已经被认为比较安全，能提供有效Dos保护的CDN中查找出可能的攻击方式实属不易。实验中还运用不同的方法模拟攻击强度。如实验一：为了获得最大的放大率，使用两个带有大字符串的cookie字段来填充4kb HTTP/2动态表。为了探讨并发流对放大率的影响，我们在一个HTTP/2连接中改变并发流的数量，并使用tcpdump捕获客户端CDN连接和CDN源连接中的流量来评估放大系数。以及在实验中尽可能地降低复杂度。
此外，实验还在6个真实的CDN供应商上执行，自建了一个自建的Apache web服务器，并将其部署为六个cdn后面的网站源，一次一个。具有很高的可信度。对于原理的分析也非常清晰，看得出作者是经过长时间地学习、分析最终达到理解、运用的效果。

#目前缺点：
与其说是缺点不如说是我对文章中不理解的地方：
1. 在实验中消耗太多的带宽，这可能会对其他CDN驱动的网站造成双边损害，并会给我们的学术界带来道德问题学习。为了解决这个问题实验中使用的是免费试用CDN帐户和默认配置进行的，那么如果攻击者拥有更高的权限会怎么样呢。
2. 实验一中使用两个带有大字符串的cookie字段来填充4kb HTTP/2动态表能否真实地模拟实际攻击中对宽带带宽放大的冲击呢。
3. 对于每种攻击并没有给出更好的解决方案，只是有缓解措施，这一点可以认为是激励更多的人来解决这些问题，也可能会被攻击者恶意利用。
