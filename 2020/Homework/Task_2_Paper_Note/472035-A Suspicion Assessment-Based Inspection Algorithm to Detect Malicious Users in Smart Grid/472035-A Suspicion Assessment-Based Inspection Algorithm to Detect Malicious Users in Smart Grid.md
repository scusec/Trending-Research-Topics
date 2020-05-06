# A Suspicion Assessment-Based Inspection Algorithm to Detect Malicious Users in Smart Grid 笔记

## 论文基本信息

- 论文标题: A Suspicion Assessment-Based Inspection Algorithm to Detect Malicious Users in Smart Grid
- 论文作者: Xiaofang Xia and Yang Xiao and Wei Liang
- 论文出处: IEEE Trans. Information Forensics and Security
- 论文链接: <https://doi.org/10.1109/TIFS.2019.2921232>
- 笔记作者: 缪昌伟

## 论文主要内容

智能电网在为用户提供巨大便利的同时面临着安全挑战，尤其是以偷电为目的的网络攻击。该论文审视了现有的针对智能电网设计的安全检查方法，发现这些方法均在检测精度和部署成本上存在较大问题。为了能够在最短的时间内，依托数量有限的监控设备较为精确地定位到攻击者（恶意用户），该论文提出了一种基于怀疑评估的检测算法。该算法可以在电网人员上面检查前，通过分析电力盗窃记录（怀疑的依据）以及电力消耗和预测值的偏差对用户偷电行为进行快速的综合评估，提高智能电网的可靠性和安全性。

## 论文创新

- 提出了基于怀疑评估的检测算法（感觉思路上和风险控制中用到的征信体系有异曲同工之处）
- 对检测设备的性能依赖低，不需要在已有智能电网中追加额外的监控设备（低成本、易部署）
- 算法开销低，不像大多数数据挖掘那样依赖海量的数据和算力

## 论文缺点

### 怀疑评估存存在潜在偏差

该论文提出的SAI检测算法的核心是怀疑评估，即依赖用户的“信用记录”对用户行为进行综合评估。换言之，该方案重度依赖用户的信用记录。和当前征信体系一样，这样的方案面临的最大问题是信用记录的合理可靠性。目前，SAI的做法主要是分析用户窃电记录、比较用户用电和预测值的偏差。这样单薄的评估角度可能不足以建立一个合理可靠的信用记录，进而导致SAI进行怀疑评估的结果存在一定偏差。

## 改进办法

### 借鉴征信评估方式，丰富信用评估维度、怀疑评估立体化

正如信用污点类型多样，偷电的形式也是五花八门（不同形式的偷电记录反应在电网数据上的形式也应该存在一些差异）。因此，可以考虑丰富对应的信用评估维度，使得用户用电信用记录立体化、合理化。例如，区分用户用电时段分布偏好、区分用户单次偷电额度区间、区分地区用电量变化周期等。这样，在实施SAI检测时，可以更加全面、合理的对用户行为进行分析，有效提高检测的准确性。