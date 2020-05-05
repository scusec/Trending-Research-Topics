## Distributed Quickest Detection of Cyber-Attacks in Smart Grid

*   本文章发表在 [IEEE Transactions on Information Forensics and Security](https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=10206) ( Volume: 13 , [Issue: 8](https://ieeexplore.ieee.org/xpl/tocresult.jsp?isnumber=8330769) , Aug. 2018 )
*   作者是来自纽约哥伦比亚大学的Mehmet Necip Kurt

----

1.  本文章主要提出了一种针对智能电网攻击（主要是假数据注入FDI和拒绝服务攻击Dos）检测提出了一种分布式的检测方法，其主要贡献在于提出了一种新的电网采样方案(level-crossing sampling with hysteresis (LCSH))以手机信息，改善了均匀时间采样(US)带来的在面对结构化攻击和随机攻击时反应速度慢的问题，并带来了更高的鲁棒性。
2.  本文的创新之处即在于LCSH的提出，其大致是(由于确实对电网不是很熟悉，一些专业词汇可能出现错误)将检测的频率在一个区间内进行调整，根据节点的cross level不同而进行不同间隔的取样。
3.  文章提出的方法适用于攻击的时间随机性较高、攻击总数量较小的情况。并且可以采取分布式或集中式的部署方法，然而，在分布式部署的情况下，其总体计算代价较大，部署成本高，并且方法本身并没有进行安全性的校验，容易受到攻击。
4.  针对上述问题，我个人认为有以下解决方案：
    1.  针对分布式部署总计算代价较大的问题，其可以加入针对电网内流量情况的监测，并根据这样的情况调整计算策略，将部分节点去除或加入计算
    2.  本方法进行的检测没有进行安全性校验，无法应对中间人等攻击，其应当在检测中加入不可重放的验证模块，而根据分布式的特点，其也可以使用同态加密等技术来保持加解密方的对称以减少计算代价，提高并发性。

