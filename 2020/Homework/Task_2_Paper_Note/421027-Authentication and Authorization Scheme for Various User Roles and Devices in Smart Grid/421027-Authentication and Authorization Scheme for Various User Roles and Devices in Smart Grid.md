
# 论文信息
1. 标题：Authentication and Authorization Scheme for Various User Roles and Devices in Smart Grid
2. 作者：Neetesh Saxena  ; Bong Jun Choi ; Rongxing Lu
School of Electrical and Electronic Engineering, Nangyang Technological University, Singapore
3. 出处和链接：IEEE  [链接](https://ieeexplore.ieee.org/document/7366583)
4. 笔记作者昵称: Jixuan Ma/马冀旋

# 主要内容
该论文提出了一种安全有效的身份验证和授权方案，通过验证用户授权并在用户访问设备时一起执行用户身份验证，来缓解智能电网中的外部和内部威胁。所提出的方案使用基于属性的访问控制来动态计算每个用户角色，并与设备一起验证用户的身份。
# 创新点
该方案可以轻松地应用于访问SG系统中不同设备的不同用户角色，因为使用了SHA256哈希的基于属性的访问控制，而且动态计算每个用户提供的（访问方式，部门，位置，SDP）属性的功能。方案启用了两因素身份验证，从而使恶意设备无法重新使用捕获的合法用户先前的信息。在用户和设备之间生成基于双线性配对密码术的共享密钥，以在会话中进行进一步的安全通信。
# 目前缺点
通信和计算开销大，效率低，密钥管理困难。

# 解决方式
改进权限控制机制。