### 关于Melting Pot of Origins: Compromising the Intermediary Web Services that Rehost Websites的论文笔记

***

+ 笔记作者：531142

+ 论文题目：Melting Pot of Origins: Compromising the Intermediary Web Services that Rehost Websites

+ 论文作者：Takuya Watanabe*∗†*, Eitaro Shioji*∗* , Mitsuaki Akiyama*∗* and Tatsuya Mori*†‡§*

  *∗*NTT Secure Platform Laboratories, Tokyo, Japan

  *†*Waseda University, Tokyo, Japan

  *‡*NICT, Tokyo, Japan

  *§*RIKEN AIP, Tokyo, Japan

+ 论文来源： NDSS 2020

  原文链接：https://www.ndss-symposium.org/ndss-paper/melting-pot-of-origins-compromising-the-intermediary-web-services-that-rehost-websites/

---

### 1.论文摘要

web服务中介（网络翻译、网络档案等中间网络服务），例如Web代理，Web翻译和Web档案已经成为人们无处不在使用的工具，极大的提高了网络的开放性，作者将这些服务称为web重新托管服务。作者认为这些服务为网络托管服务，作者对这些服务进行了首次大规模漏洞研究。作者发现了五个不同种类型的攻击：持续的中间人攻击，滥用特权以访问各种资源，偷盗身份信息，偷盗浏览器历史记录和会话劫持或者注入。

***

### 2.论文主要内容

作者在本篇论文中研究的主要对象是三个网络托管服务，它们分别是：web proxy, web translator, web archive。

网络托管服务增强了网络的可访问性，由于用户可能会在网络托管服务上输入隐私信息，因此攻击者可能会产生利用网络托管服务的动机。本篇文章是第一次针对具有托管属性的网站进行大规模的研究，并发现常见的安全问题。并且基于此问题，作者提出了一个PoC攻击模型，并验证了其可行性。

攻击的核心想法利用了一个事实由网络托管服务提供的域名是可以被用来访问各种托管网站的；这种“melting pot of origins”情况允许攻击者绕开同源安全策略的过滤。通过使用这种攻击，作者发现可以展开多种攻击。作者又进一步检查了21中流行的web托管服务并检查是否存在这种漏洞。作者发现其中19个存在。以下是论文中对这些网络托管服务的具体分析：

##### 先进的网络服务所具有的特征

- **Service Worker**是现代web的一个特征。它是JS写的一个事件驱动的web worker。它与主浏览器线程独立工作，并提供丰富的功能，例如后台数据同步和推送通知处理。Service Worker的一个显着特征是它可以代理Web客户端和服务器之间的所有请求和响应，并修改内容。
- **Application Cache**是 HTML5标准提供了一套应用程序缓存机制，这允许web应用程序离线运行。
- **Browser Permissions** 使得web浏览器支持访问各种各样的资源，如地理定、相机、麦克风等，访问这些资源需要用户的许可。这里有一个假设，就是不同的域名运行着不同的访问资源策略。然而，通过Web托管服务授予的访问权限违反了此假设。

##### 攻击所需Cookies的缺陷

- **Access from** JS 如果设置了HttpOnly标志，且HttpOnly成功的话，那么JS脚本就不可以接触到Cookie，但是大部分网站这个标志被设置为false。
- **Session Cookie** 如果没有设置过期的日期，那么cookie会变成会话cookie，技术上来讲会话cookie会在浏览器关闭后被删除。但是实际上，在浏览器中配置“Continue where you left off”设置将使会话保持活动状态。
- **Cookie Bomb Web**服务器拒绝那些请求头太大的请求。如果对于一个网站有太多太大的cookies，服务器通常会返回一个错误。

##### 攻击过程

- 攻击者构造URL为https://rehosted.example/rehost?url=https://evil.example的包含恶意脚本的网页，并使其运行。
- 攻击者通过传统的Web攻击场景（下载、网络钓鱼和跨站点请求伪造，垃圾邮件，恶意媒体链接的帖子）诱导受害者访问恶意页面。这里需要注意，某些网络重新托管服务会通过验证引荐来源网址或HTTP会话来禁止进行热链接（即直接链接到重新托管的页面），这增加了攻击的攻击的难度。

- 触发攻击

为了使得攻击更加有效，攻击者可以使用一个登录页面，这个页面嵌入的多种iframe标签指向由各种web托管服务代理的恶意页面。通过单独访问这一个页面，攻击者便可实现利用多个托管服务实现攻击的场景。而这个登陆页面时不需要被托管的。对于模拟域名有几种选择：通过缩短的URL进行包装或重定向服务，并通过XSS和网站伪造将其注入合法站点。

![image-20200505215803441](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200505215803441.png)

---

### 3.论文创新点

1. 作者在Coverage of Our Experiments 分析了它检查的web托管服务的全面性，并加以分析。
2. 作者提出了一个通常存在于这些服务中的严重威胁，并证明了许多服务实际上是脆弱的。另一方面，作者并没有从用户实际使用这些服务的角度来考察。但是作者给出了充分的实例，说明他们的假设是成立的。
3. 作者在文章中总结了5种现存的防御方式。
4. 作者提到了现在的浏览器是无法做到快速对Service Worker检查的。

---

### 4.论文评论

文章研究的方面不是一个被广泛讨论的话题，对于刚开始接触这个问题的新手需要花很多时间来了解论文中的相关知识。需要完全理解该论文中的内容需要对网络由比较充分的了解。另一方面，文中的各种插图也帮助读者能够更好的了解一些特定的内容。作者发现谷歌翻译有一个特点，就是会翻译用户上传的文档。如果这个页面包含漏洞，并且存在长久的service worker，那么攻击者可能会盗取用户文档中的信息。但是对service worker无法快速检查没有提出有效的解决方法。
