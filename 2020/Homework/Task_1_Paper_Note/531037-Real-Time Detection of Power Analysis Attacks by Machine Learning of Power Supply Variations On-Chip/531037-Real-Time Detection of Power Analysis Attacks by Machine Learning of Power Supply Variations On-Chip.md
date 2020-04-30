# 论文信息

标题：Real-Time Detection of Power Analysis Attacks by Machine Learning of Power Supply Variations On-Chip

作者：Dmitry Utyamishev, Inna Partin-Vaisband

出处：IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems ( Volume: 39 , Issue: 1 , Jan. 2020 )

链接：<a href="https://ieeexplore.ieee.org/document/8552470">https://ieeexplore.ieee.org/document/8552470</a>

# 论文简要、框图、主要内容

功耗攻击(power analysis attack, PAA)：功率分析攻击是一种测信道攻击，利用芯片在进行某些特定运算时功耗会发生变化的特性，以分析芯片正在进行的工作。

典型的PAA为使用探头外部连接到芯片，然后恶意地感应电压和电流信息。

通过大量输入序列测试系统行为和相应功率分布之间的关系，应用统计学或者机器学习方法，窃取芯片内的信息，如加密算法。常用攻击手法有模板攻击、随机攻击、机器学习攻击、简单功率分析、相关功率分析和差分功率分析。

传统的PAA防护方法为削弱功率分布和系统行为之间的关联，或者功率隐藏与功率隐蔽。这些方法在已经被证明有效的解决方式。

然而，已有的PAA防护策略会降低密码系统的性能。基于现有的恶意探测的外接电阻会影响密码系统的物理阻抗特性这一特点，本文提出的方法可以揭示非典型的电压变化，以识别恶意探针。

识别到恶意探针后，可以停止敏感数据操作、报告系统、或激活其他对策。

# 创新点

+ 本文另辟蹊径，从硬件安全的攻击层面反向思考了受到攻击会导致什么样的异常，通过检测异常以及对异常进行特殊处理。

# 缺点

+ 本文的亮点在于降低功耗，但是没有鲜明的数据图标以体现这一优势
