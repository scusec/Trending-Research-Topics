## "ShellBreaker：Automatically detecting PHP-based malicious web shells" 论文笔记

论文题目：ShellBreaker：Automatically detecting PHP-based malicious web shells

论文作者：Yu Li, Jin Huang, Ademola lkusan, Milliken Mitchell, Junjie Zhang, Rui Dai

笔记作者：Matchtheworld

[原文链接](https://www.sciencedirect.com/science/article/pii/S0167404819301506)

### 论文笔记信息

---

#### 1. 研究背景

​	Web Shell是攻击者上载到受感染Web服务器的服务器端脚本，旨在启用对受感染计算机的持久访问。在许多利用活动之后，例如SQL注入，远程文件包含（RFI），无限制文件上传和跨站点脚本（XSS），它充当了利用后阶段。因此，考虑到Web服务的广泛普及以及据报道它们易受攻击的可能性，检测Web Shell至关重要。在这篇论文中，作者提出了一个名为ShellBreaker的新颖系统， 用于检测用PHP编写的Web Shell，PHP是用于服务器端脚本开发的主要语言之一。

#### 2. 研究内容

​	作者设计了一个名为*ShellBreaker*的系统来检测恶意Web Shell。下图展示了*ShellBreaker*的体系结构概述。*ShellBreaker*并没有分析PHP脚本的源代码，而是首先利用解析器生成抽象语法树（AST）。与原始源代码相比，基于AST的表示形式不仅排除了编程的变体，例如注释，空格等，而且还显示了脚本结构。 *ShellBreaker*基于派生的AST进行语法和语义分析。

- 遍历AST以识别结构感知的语言功能，例如敏感的API以及这些API与特定语句之间的关联。
- 实现了对AST进行轻量级污点分析的解释器，旨在揭示和表征从超全局变量到敏感操作的显式和隐式数据流。

![](https://github.com/scusec/Trending-Research-Topics/blob/master/2020/Homework/Task_1_Paper_Note/531021-ShellBreaker%20Automatically%20detecting%20PHP-based%20malicious%20web%20shells/The%20architectural%20overview%20of%20SheelBreaker.png)

#### 3.主要内容

​	为了设计能够有效区分恶意Web Shell，作者提出了八个的检测的特征来用于检测。

> - **超级全局变量的数量**。在脚本中，我们计算超全局变量的数量，包括:
>
>   \$\_GET,\$\_POST,\$\_FILES,\$\_COOKIE,\$\_REQUEST,\$\_SERVER,\$\_SESSION。
>
> - **条件语句的百分比**。此功能描述了条件语句的数量，包括脚本中语句总数的 if， elseif， else， case和三元符号。
>
> - **每种情况下平均二进制操作数**。对于每个脚本，我们计算二进制运算（例如 &&， >，）的数量。和 =在脚本中，然后除以条件语句的总数，包括 if， elseif， else， case和三元符号。
>
> - **循环语句的百分比**。此功能测量循环语句（包括 while，for和 foreach）在脚本中语句总数中所占的百分比。
>
> - **字符串数**。在脚本中，我们计算字符串的数量。
>
> - **最长的字符串的长度**。在脚本中，我们测量每个字符串的长度，并使用最大的字符串作为特征。
>
> - **显性数据流**。此功能度量其敏感参数通过数据流被超全局变量污染的敏感操作的数量（即，敏感操作和超全局变量之间存在数据相关性）。
>
> - **隐式数据流**。此功能可度量属于执行路径的敏感函数调用的数量，这些执行路径由超全局变量污染的变量控制。

#### 4. 创新点

- 提出了两个新的检测webshell的特征：显性数据流和隐式数据流。
- 提高攻击者的门槛，减少超全局变量的使用将限制将命令和参数传输到Web Shell的带宽。减少分支和循环语句将分别降低Shell的适应性和自动化程度。从超全局变量到敏感操作的数据流中断将立即阻止恶意Web Shell的使用。

#### 5. 目前的缺点

- 一旦攻击者知道ShellBreaker的设计  ，他们就可以尝试通过更改Web Shell的行为来逃避检测。
- 论文提出的ShellBreaker系统的当前实现的检测仅限于单个PHP脚本，而不管它可能与其他脚本是否发生交互。

