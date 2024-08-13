---
title: 一生只记一个密码： 1Password 简明教程
description: ''
date: 'Sat Jan 27 2024 22:50:02 GMT+0800 (中国标准时间)'
dateFormatted: 'Sat Jan 27 2024 22:50:02 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# 转载：[一生只记一个密码： 1Password 简明教程](https://yishi.io/1password-complete-tutorial/)

By [王一石](https://yishi.io/author/

> _**本文将严格按照初次接触 1Password 的普通用户视角，带大家过一遍 1Password 使用的最佳实践。如果你以前用过或熟悉
> 1Password，可以略过入门部分，直接挑选对你有用的内容查阅；**_
>
>  _文中截图使用的是 1Passwrod for Mac 桌面端，操作环境是 macOS Catalina。如果你平时使用 Windows
> 的话也无需担心，两者操作界面几乎一致，使用逻辑也没有区别，这份教程对你同样适用。1Password 支持包括
> macOS、iOS、Windows、Android、Linux、Chrome OS、命令行等全平台；_
>
>  _示例账户遵循 1Password 官方推荐的使用方式，选择的是「订阅制」，并使用云服务器同步账户信息。除了介绍主流的 1Password
> 使用方式，本文中我还会详细讲解「 **创建和同步独立保险库」、「数据导入及导出」、「加密及关联文件」** 等衍生功能。 **掌握这些方法，你可以做到对
> 1Password 运用自如，进而提升自己对账户安全的掌控力。**_

### 什么是 1Password

1Password 是由加拿大开发商 [AgileBits](https://1password.com/company/)
开发的一款密码管理软件。除了用来存放账号密码，你还可以存放包括信用卡、身份证件之类的敏感信息。根据官方的[发行公告](https://app-
updates.agilebits.com/product_history/OPM2#2352)（Release Notes），第一个正式版的
1Password 1.0.0 客户端发行于2006年，距今14年。

**我们储存在 1Password 中的信息都是被加密的，任何数据在被传输前，1Password 都会使用 AES 256-bit
算法加密3次，即便是开发商 AgileBits 也无法获取。客户端和 1Password 服务器的认证和通信通过零知识证明协议加密。**

2014年 OpenSSL
暴露的[心脏滴血漏洞](https://heartbleed.com/)（Heartbleed）漏洞对整个互联网造成了难以估量的影响，所有依赖
SSL/TLS 协议的网站或客户端，都可能因此受到攻击。 **当时很多使用 OpenSSL 服务的科技巨头（e.g. Google, Facebook,
Amazon 以及国内各梯队的互联网公司等…）的用户敏感数据被大量 Dump，其中有不少公司甚至明文保存用户密码。** 如果你愿意了解更多细节，可以搜下
"Akamai secure heap “，Alex Clemmer 专门写了[文章](https://blog.nullspace.io/akamai-
ssl-patch.html)来分析这件事，过程很是曲折。

所幸 1Password 并不建立在 SSL/TLS 之上，因此[并未受到波及](https://blog.1password.com/imagine-
no-ssl-encryption-its-scary-if-you-
try/)，官方不久后还推出[暸望塔](https://support.1password.com/watchtower/)（Watchtower）功能，用来检查你使用过的哪些网站遭到数据泄露，这个功能不久后就集成到客户端中。

**1Password 的盈利模式完全来自用户付费，因此他们没有任何第三方广告业务，也不使用、分享或出售用户数据。** 1Password
严格遵守欧盟数据保护通用条例
GDPR，他们在官网隐私介绍页面详细说明了[隐私策略](https://support.1password.com/1password-privacy/)。

苹果在2018年为全球超过123,000员工[部署企业版1Password](https://bgr.com/2018/07/10/apple-1password-
acquisition-deal/)。

### 为什么要用 1Password

这个问题可以拆成两部分：

**1）为什么要使用「密码管理器」；  
2）为什么要在众多密码管理器中选择  1Password？ **

对问题1，很多人习惯在所有网站都使用相同密码，而且通常包含生日年月这样非常容易被外人获得的信息。
**一旦其中某个网站发生数据泄露，你所有的账户都会受到牵连。** 即便能做到不同账号不同密码，我们为了方便记忆，设定的密码也往往强度不足。

通常，高强度的好密码要满足：

  * 长度8位及以上； 
  * 同时包含大写字母和小写字母； 
  * 包含1及以上的特殊符号（e.g. *^%$=…）； 
  * 自己能记住。 

在使用密码管理器之前，我曾一直用「基本密码」+「特征码」来设置密码，并为此感到洋洋得意。以 Gmail 账户举例，我以基本密码 "Yishi123+-/"
\+ 特征码 “GL"（网站域名的首尾大写字母）作为密码  "Yishi123+-/GL"；如果账户涉及财产，就换个更长的基本密码。

乍一看符合好密码的要求，自己也能记住，看起来比所有网站同用一个密码要强多了不是么。 **但这样做最多在黑客批量撞库时躲过一劫，实则没什么作用** 。

因为只要黑客通过社工手段定位到你个人，不管你以什么方式组合特征码、特征码有多复杂，只要规则一致的，那么其中一个账号被盗，其他的就都能顺藤摸瓜推理出来。

**因此，所谓基本密码+特征码，在安全性上形同虚设。**

有人说，那我每个网站都使用毫无规律的随机长密码。拿小本子把账号密码都记下来，按字母 a-z
给网站排序，每次登录时查下不就行了。除非本子遗失或黑客到家里盗走，我的密码都是万无一失的，也不怕撞库。

这个办法安全系数确实最高。某种程度上，小本子就是你自制的密码管理器，但是用起来麻烦。

小本子丢了或损坏怎么办，人在公开场所怎么办，每天登N个网站就要手动敲N遍毫无规律的密码，诸如此类的缺点很多，余不一一…

而一个专业的密码管理器，就是用来解决这个问题的。

它本质上做了两件事：

  1. **帮你生成足够强的随机密码；**
  2.  **帮你管理好这些账户，要用时出现，不用时消失。**

对问题2，我亲身使用过的密码管理器有 1Password、LastPass,、KeePass，除此之外还有一大票优秀产品如 DashLane,
RoboForm … 等，虽然没用过，但它们都有各自粉丝拥簇。

**如果你喜欢彻底开源、轻量、免费，那么我强烈推荐[KeePass](https://keepass.info/)，它的开发社区很活跃，光是在 macOS
上，开发者们就贡献了 KyPass，MacPass，KeePassX 等多个客户端的实现，并且功能十分强大。 **

**但如果你和我一样，除了安全性，同样在意使用体验、灵活性和便利性，本着「能力范围内选择综合素质最好的」原则，那么我推荐 1Password。**

1Password 并非开源，但它遵循公开规范（[安全模型的白皮书](https://1password.com/files/1Password-
White-Paper.pdf)），任何开发者都可以对其进行黑箱测试。

David Schuetz 在他的[博客](https://darthnull.org/security/2018/11/09/1pass-misc/)对
1Password 的工作机制进行了极为详尽的探索，下图便是他总结的核心：

![](https://yishi.io/wp-content/uploads/2020/03/image-6.png)

我们只需明白，1Password 最关键的安全要素，便是我在图中红框标出的 2SKD（two-secret key derivation）。
**而这两个所谓的 “Secret key "，分别是主密码（Master password）和 私钥（Secret
key）。**你不用看懂这套复杂的流程，只要抓住核心点，即，如何确保「我的密码只有我知道，即便1Password
也无法查看我的敏感信息」即可。关于这点，我会在下文设置主密码的步骤中，详细跟你解释。

开源是个很大的话题，它也并非一切事物的银弹。受制于篇幅，本文我们主要讲解 1Password 的使用，如果你对开源感兴趣，以后可以单独写一篇文章。

**准备就绪，接下来就开始我们的 1Password 之旅。**

### 注册账户

**登陆 1Password
官方网站：[点击访问](https://www.tkqlhce.com/click-9258661-13433658?url=https%3A%2F%2F1password.com%2Fzh-
cn%2F)**

点击「免费试用」，1Password 支持30天免费试用， **只需要一个邮箱，不需要绑定信用卡。**

![](https://yishi.io/wp-
content/uploads/2020/02/截屏2020-02-26下午7.37.04-1024x921.png)

选择「个人&家庭」，点击「免费试用30天」。

![](https://yishi.io/wp-content/uploads/2020/03/image-35-1024x921.png)

**1Password 有两种付费方案，一种是买断制，一种是订阅制。**

**对于买断制（Standalone），每个平台客户端单独购买，终身使用，但遇到大版本更新可能需要付费升级，不升级依然可以继续使用。** 1Password
过去的 4、5、6 大版本都是直接免费升级，非常良心，但或许是迫于营收压力，从 6 升级到 7，需要支付49美金。  

**对于订阅制（Subscription），可以按月或按年付费，不限平台及设备数量，实时更新最新版本。** 这是 1Password
目前主推的付费方式，每月2.99美金；如果是家庭一起用，价格就更美丽，人均每月不到1美金。

未来 1Password 应该不会再推出买断制的版本，现有的付费升级也是给老用户一个可选项。如果你想使用支持买断制的老版本
1Password，可以去官网下载，macOS 系统下最新版本是 [1Password 6.8.9](https://app-
updates.agilebits.com/download/OPM4)，Windows 系统下最新版本是 [1Password
4.6.2](https://c.1password.com/dist/1P/win4/1Password-4.6.2.626.exe)。

**关于购买的建议：**

  * **不要贪图便宜去某宝买，基本是黑卡，一旦被查明，无理由封号；**
  *  **不要和外人共用家庭账户，密码是敏感信息，家庭账户管理员可以恢复成员被删的内容，有安全隐患；**
  *  **不要使用任何来源的所谓破解版，因为你根本不知道里面是否有后门或木马，如果你不想为正版付费，那么我推荐使用  [KeePass](https://keepass.info/)，开源、免费。 **

继续注册，输入你的昵称，以及邮箱地址。 为了避免邮件推送对用户的干扰，1Password 默认取消邮件订阅的选项，我们保持原状就好。

![](https://yishi.io/wp-content/uploads/2020/03/image-37-1024x781.png)

输入 1Password 发送到你邮箱的6位数字确认码。

![](https://yishi.io/wp-content/uploads/2020/03/image-39-1024x781.png)

点击底部的「稍后添加卡片」，我们暂时只想试用。

![](https://yishi.io/wp-content/uploads/2020/03/image-38-1024x781.png)

**设置主密码，这是最核心的密码，它应该不同于你在其他任何平台使用过的密码。万一遗忘，1Password 也无法帮你找回，因此务必慎重。**
主密码在设置后随时可更改，不限次数，但前提是你记得原主密码。

设置主密码有几个[原则](https://support.1password.com/strong-master-password/)：

  * 你的主密码是独一无二的； 
  * 你的主密码是没有明显规律的； 
  * 你的主密码是自己能记住的。 

**你应该对自己的主密码负责，确保它牢牢存在你的脑子里。**

![](https://yishi.io/wp-content/uploads/2020/03/image-36-1024x781.png)

成功登陆 1Password，将 Secret key 下载到本地，先不用管它，我稍后会解释这个要如何使用。

![](https://yishi.io/wp-content/uploads/2020/03/image-31-1024x781.png)

点击「获取应用」，选择你目前使用的操作系统，安装 1Password。

![](https://yishi.io/wp-content/uploads/2020/03/image-24-1024x781.png)

### 开启 1Password

恭喜，你已经完成了所有准备工作。打开刚刚安装好的 1Password，你会发现有一些信息已经被预先填好，有一些则需要你主动填写。 **还记得我们提到过的
2SKD（two-secret key derivation）、Secret key 等一系列名词吗？是时候跟你解释了。**

下图中示例账户信息从上往下分别是：

  1. Web 版 1Password 登陆地址：my.1paasword.com 
  2. 你的登陆账户名：yishi01.wang@outlook.com 
  3. 你的私钥 Secret key：A3-WXH7FN-MQNQGZ-…. 
  4. 你的主密码：********* 

![](https://yishi.io/wp-content/uploads/2020/03/截屏2020-02-26下午9.50.22.png)

所谓 2SKD（two-secret key derivation）机制，指的是1Password 同时使用你自己设定的主密码（Master
password）和私钥（Secret key）来加密你的信息，以及在与服务器通信的过程中验证你的身份。

**主密码（Master password）不会被 1Password 存储，它只有在被运行的时候短暂存在于机器的内存中。**

**Secret key（即图中的 Account key）在且仅在本地生成，不会上传到服务器。**

![](https://yishi.io/wp-content/uploads/2020/03/image-1.png)

因此，如果有一天你忘记了主密码或私钥中的任何一个，那么你将再也无法恢复你存储的所有账户信息，所以务必要保管好。

还记得刚才登录 1Password 网页后，下载到本地的一份 PDF 吗？这就是 1Password 急救包（Emergency kit），你有两种选择：

  1. 将它打印出来，然后放到安全的地方。以防有天突然忘记主密码，你可以在图中框出的地方，将你的主密码写上作为备份。 
  2. 将它存放在 U 盘里，然后放到安全的地方。 

总之，不要将它发到网上，也不要拍照传到云相册。

![](https://yishi.io/wp-content/uploads/2020/03/image-33-829x1024.png)

终于来到主界面了，欢迎页面的这几个快捷选项，你以后随时可以设置，现在我们直接进入。

![](https://yishi.io/wp-content/uploads/2020/03/截屏2020-02-26下午9.51.34.png)

### 创建登陆信息

不出意外的话，你看到的界面应该和下图没有差别。1Password 客户端从左至右依次是：侧边栏、账号列表、账号详情，
**它们从逻辑上是依次递进的，你在侧边栏过滤，在账号列表选择，在详情页面查看、编辑或分享。**

**从现在起，我说的账号指的都是在 1Password 中保管着的，你其他网站或 App 的账号，而不是你的 1Password 账号。你的
1Password 账户，就是我们在本文一开始注册 1Password 使用的邮箱，不要搞混。**

![](https://yishi.io/wp-
content/uploads/2020/03/截屏2020-02-26下午10.19.35-1024x728.png)

1Password
预设了非常多的信息类型，最常用的有「登录信息」、「安全备注」、「身份标识」等，这些类型实际上都是模板，由不同的表单组成，你可以随意组合或添加新的字段、组别等等，等我们走完最基础的使用流程，我会教你如何玩出「新花样」。

![](https://yishi.io/wp-content/uploads/2020/03/image.png)

现在跟我创建第一条账号信息吧，比如我希望在 1Password 保存我的 Outlook 邮箱账号：

  1. 点击「创建新条目」按钮 
  2. 将「登录信息」标题改为 yishi@outlook 
  3. 填入用户名：yishi01.wang@outlook.com 
  4. 填入密码 
  5. 填入网站地址：outlook.com 

点击保存，就这么简单。

每次给账号起标题时，我都是以「账号名@网站」的形式命名，例如我有两个 Outlook 邮箱，用户名分别是 yishi01.wang 和
bar01.wang，那么我会以 "yishi@outlook”，"bar@outlook” 分别命名。 **这样每次要找账号时，只要在 1Password
全局搜索框输入几个字母就可以迅速定位，节约大量时间。**

眼尖的你可能已经在疑惑，下图中的「重新生成密码」和右侧蓝色的小齿轮是做什么用的。其实这是 1Password
自带的密码生成器，每次你创建新账号或编辑老账号时，只要点击小齿轮，密码生成器就会弹出。

上面3个拖拽条可以分别控制生成密码的：

  * **长度，即位数；**
  *  **密码中包含的数字个数；**
  *  **密码中包含的符号个数。**

这个功能最好的地方就在于， **不同的网站往往有不同的密码要求**
。有的要求密码必须大于8位，有的要求必须带有数字或符号等等。你可以根据需求生成想要的密码，而不用像以前一样绞尽脑汁，好不容易想到合适的密码，却在填完后转头就忘。1Password
还提供免费的[网页版密码生成器](https://1password.com/zh-cn/password-
generator/)，如果读到这里你还没在本地安装 1Password 软件的话，不妨在网页上玩玩看。

![](https://yishi.io/wp-content/uploads/2020/03/image-18-1024x728.png)

### 掌握 1Password 正确的使用方式

刚才我们已经成功创建了第一个账号，很简单吧。

但是你可能会冒出新问题，自己以前的那么多网站账号该怎么办，难道要手动一个个敲进去吗；另外，平时注册网站时都是在网页上操作，以后每次要在网页上输一遍，然后打开
1Password 再输一遍吗？

当然不是。

要快速导入已有的账号，可以通过 1Password 官方导入工具，目前支持
1Password、LastPass、Dashlane、RoboForm、Chrome，点击对应的数据源，按照网站提示一步步操作即可。

![](https://yishi.io/wp-
content/uploads/2020/03/截屏2020-02-2919.51.52-1024x949.png)

如果上面的数据源都不符合，你还可以自行制作 CSV 文件来批量导入（Excel 可以导出 CSV 格式），
**只需要确保[内容格式](https://support.1password.com/create-csv-files/)跟 1Password
所要求的匹配**。不过我不打算在这里展开，因为大部分人使用的密码数量都很有限，与其慢慢重新整理再导入，不如在 1Password 里直接创建更直观。

![](https://yishi.io/wp-content/uploads/2020/03/image-22-1024x949.png)

**针对原先已存在的各种网站账号，我建议在你登录这个网站时把账号信息直接同步到 1Password，登录即保存，省去在软件重新输入的烦恼。**
既然要跟网站打交道，是时候请出 1Password 的得力助手了。

### 1Password 官方浏览器插件

如果你使用 macOS 系统，那么在你安装完 1Password 软件后，Safari 浏览器就已经内置了插件，你只需要打开它即可。

点击桌面左上角，选择 1Password 的「偏好设置」。

![](https://yishi.io/wp-content/uploads/2020/03/image-30.png)

点击顶部的「浏览器」标签页，确保你勾选了「始终保持 1Password 扩展助手运行」这个选项。

![](https://yishi.io/wp-content/uploads/2020/03/image-4.png)

接下来，打开你的 Safari 浏览器，点击桌面菜单栏左上角 Safari 的「偏好设置」，快捷键是 Command + 英文逗号 “⌘ ,”
。确保你勾选了 1Password 扩展，允许它访问你的登录信息等。

![](https://yishi.io/wp-content/uploads/2020/03/image-12.png)

现在你已经可以在 Safari 中使用 1Password 插件了，注意观察，在你的浏览器地址栏旁边出现了 1Password
的标志。你可以随时点击它唤起 1Password，帮你在网页中填入账号信息等等。

![](https://yishi.io/wp-content/uploads/2020/03/image-11.png)

如果你使用的是 Windows 系统，或者使用 macOS 系统但并不常用 Safari，你可以安装其他浏览器插件。以下是 1Password
官方支持的[全部浏览器](https://1password.com/zh-cn/downloads/mac/#browsers)：

  * Google Chrome
  * Firefox
  * Brave
  * Microsof Edge

接下来我将以 Chrome 浏览器的 1Password X 插件为例，继续我们的探索。  
要事先说明的是，1Password 的浏览器插件有两种类型，分别是独立型的 1Password X 和依赖本地软件的插件。

**所谓独立型，就是不需要在本地额外安装 1Password，在浏览器上就可以完成 1Password 几乎所有功能；**

**而依赖型插件，则要求本地安装 1Password，它通过接口和你本地的 1Password 交换数据，是你在浏览器中使用 1Password
的延伸，刚才我们在 Safari 打开的插件，就是这种类型。**

相比依赖型插件，独立型的 1Password X 更为强大和智能，也是目前官方推荐的在浏览器中使用 1Password 的方式。

因为数据都是实时同步，你可以同时使用本地 1Password 客户端 和 1Password X，我自己也是这样做的，怎么方便怎么来。

![](https://yishi.io/wp-content/uploads/2020/03/image-32-1024x781.png)

现在进行安装。因为众所周知的原因，某些地区不能访问 Chrome 应用商店，因此你需要自备道具。 我假设你已经成功使用道具完成翻跃，现在看到的就是
[1Password X
插件的详情页面](https://chrome.google.com/webstore/detail/1password-x-%E2%80%93-password-
ma/aeblfdkhhhdcdjpifhhbdiojplfjncoa?utm_source=chrome-ntp-icon)。

![](https://yishi.io/wp-content/uploads/2020/03/image-34-1024x947.png)

插件成功安装后，点击「登录」按钮。

![](https://yishi.io/wp-content/uploads/2020/03/image-21-1024x947.png)

还是熟悉的味道，回忆一下，我们之前已经在本地桌面端的 1Password 中输入过这些信息了，这里的登录和上一次没有任何区别。1Password
已经贴心的帮你填好一些内容，因为这些数据本就缓存在你本地。

![](https://yishi.io/wp-content/uploads/2020/03/image-23-1024x947.png)

搞定了，是不是比想象的要容易。

![](https://yishi.io/wp-content/uploads/2020/03/image-2.png)

现在让我们看看插件有什么魔力。 **只要你在 1Password 保存了相应网站的账号，每次登录时，登录界面上都会出现 1Password
的标志。点击后，1Password 就在对应位置弹出所有相关账号，选择你要登录的账号，嗖，完成。**

![](https://yishi.io/wp-content/uploads/2020/03/ezgif.com-optimize.gif)

已经在 1Password 储存的账号，快速登录是没问题了；没在 1Password 储存的老账号，还有新注册账号又要如何同步？

一点也不难，不管你是登录原有账号，或是注册新号， **只要在界面的输入框旁点击 1Password 图标，再点击「在 1Password
中保存」，1Password 就会自动把这个网站的账号、密码、网址、标题同步到你数据库。**

![](https://yishi.io/wp-
content/uploads/2020/03/截屏2020-02-26下午10.59.02-1024x1010.png)

在弹出的提示框中，你可以设定这个账号的标题，以及它要保存在哪个「保险库」中，关于保险库的概念，下文会解释，我们现在点「保存」，完成。

![](https://yishi.io/wp-
content/uploads/2020/03/截屏2020-02-26下午10.59.08-1024x1010.png)

回顾下我们现在学会的：

  * **了解 1Password 的基本工作原理**
  *  **注册 1Password 账号**
  *  **下载并安装 1Password 客户端**
  *  **清楚主密码（Master password）和私钥（Secret key）的含义，妥善设置和保管**
  *  **批量导入其他数据源的账号密码**
  *  **开启1Password Safari 浏览器扩展 / 安装 Chrome 浏览器扩展**
  *  **使用 1Password 自动登录网站**
  *  **在 1Password 自动同步老账号或新注册网站的账号**

每次登录网站时，让 1Password
帮我们填写账号，省去每天重复敲打键盘，解放双手，新旧网站的账号也可以实时同步保存，使用随机生成的强密码，安全性也能得到保障。

**看到这里，你已经掌握了 1Password 主流使用方式，无需担心账号如何同步，资料如何备份，因为这一切 1Password
已经帮你打理的服帖，至于剩下的细枝末节，今后可以慢慢摸索。**

我们现在可以尽情享受 1Password 带来的好处了。 但对于想要深入挖掘 1Password 的人来说，这会远远不够。接下来，我们要拓宽视野范围，探明
1Password 还有哪些实用的特性，有些可能稍微复杂，如果你感兴趣，就跟我来。

### 使用 1Password 双重验证

你肯定听过或使用过「双要素验证（Two-factor authentication）」，也称 2FA 或二次验证。它是基于时间、Token
等自然变量结合一定加密算法组合出一组动态密码，通常每60秒刷新一次，很难获取或破解。 **我们在一些网站的安全设置看到的二次验证，基本都是 TOTP
动态密码（Time-based one-time password）验证。**

以下图中示例的微软账户二次验证为例， **点击浏览器右上角的 1Password 图标，在弹窗中点击「二维码图标」，1Password 会自动识别当前网页的
TOTP 配对二维码，完成识别后会自动保存并提醒你。**

你在图中看到的1Password 插件显示的「一次性密码」，即为 TOTP 动态密码。只要设置完成，以后再登录对应网站，1Password
不仅帮你自动填写登录信息，连动态密码也不用你烦心。

当然，如果你不喜欢 1Password 自动填写动态密码，可以选择 Authy 或其他动态密码管理软件，这里不再赘述。

![](https://yishi.io/wp-content/uploads/2020/03/image-5-1024x828.png)

### 创建本地独立保险库

尽管我们已知 1Password 的数据通过 AES-256
算法端到端加密，也看到了官方公布的[安全模型](https://support.1password.com/1password-
security/)。但你不能否认，人的安全感最终来自对事物的完全掌控，如果我就是不信任 1Password
服务器，有没有办法既让数据全部留在本地，又不妨碍但我们继续使用它这些好用的功能和浏览器插件？

**有的，创建一个只属于你自己的保险库。**

保险库是 1Password 重要的一个概念，它跟现实世界中的「保险库」含义是相似的。它是 1Password 创造的一种特殊文件，内部使用 JSON
作为信息格式，使用 PBKDF2 作为密钥派生（Key derivation）的方式。
**你的各类账号信息都存储在保险库里，保险库经过加密后其他人无法开启。**

我们在一开始创建登录信息时，默认保存账号的保险库就已经在 1Password 服务器上托管。 **现在我们要做的，是在本地创建不与外界联网的独立保险库。**
理论上，你可以在 1Password 有无数个保险库，但我觉得那样做无必要，大部分人只需要一个保险库。

我们开始吧，进入 1Password 的偏好设置，找到「高级」选项，确保你勾选了「允许在 1Password  账户之外创建保险库」。

![](https://yishi.io/wp-content/uploads/2020/03/image-25.png)

一旦你勾选了这个选项，在你的 1Password 中会即刻出现一个新的保险库。 **现在你有了两个保险库，一个是存储在 1Password
官方服务器的保险库，一个是只存储在你本地的保险库。** 这个新的保险库使用的是同样的主密码，但不会以任何方式跟外部同步数据（除非你自行设置）。

![](https://yishi.io/wp-content/uploads/2020/03/image-26-1024x691.png)

如果你想要一个可以设置独立主密码的保险库，可以在桌面左上方点击 1Password 的文件按钮，选择新建独立保险库。

![](https://yishi.io/wp-content/uploads/2020/03/image-27.png)

这时就可以为这个新保险库设置完全不同的主密码，相应的， **要想打开这个保险库，每次都需要输入对应的主密码。**

![](https://yishi.io/wp-content/uploads/2020/03/image-16-1024x691.png)

### 同步独立保险库

本地创建的独立保险库，要如何在其他设备使用呢。比如我想在手机使用存储在家中电脑 1Password 保管的账号，就必须想办法将保险库同步过来。

1Password 支持多种保险库同步方式：

  * iCloud 同步（限 Apple 设备） 
  * Dropbox 同步 
  * 文件夹同步 

其实三者大同小异，依据个人偏好选择就可以。以「文件夹同步」为例，1Password 要求你指定一个存放保险库副本的位置，我
**建议你放在一个不容易误删的路径** ，这里我为了方便演示，随手选择了桌面。

![](https://yishi.io/wp-content/uploads/2020/03/截屏2020-02-26下午11.25.05.png)

创建完成后，你可以看到对应的文件夹中多了一个后缀为 .opvault 的文件，这个就是所谓的保险库。

而 OPVault，正是 AgileBits 为 1Password 开发的保险库文件制式，其前身是 [Agile
Keychain](https://support.1password.com/cs/agile-keychain-design/)，作为目前
1Password 默认的保险库格式，它的性能和安全性相比之前得到了很大提升，
**其中一些关键特性并不止足当前，而是作为前瞻性的设计防范未来可能出现的风险** 。

你可以用任何第三方工具同步这个文件夹，甚至用 U 盘拷贝粘贴都没问题， **所有以上提及的同步方式，都不经过 1Password 服务器。**

![](https://yishi.io/wp-content/uploads/2020/03/image-13.png)

除此之外，1Password 还支持局域网同步。你可以将本机设定为 WLAN 服务器，打开后，只要在你手机 1Password 的设置项中选择「与 WLAN
服务器同步」，选中本机的设备名称，输入窗口中显示的密钥即可完成同步。这种方式对安卓手机同样适用。

![](https://yishi.io/wp-content/uploads/2020/03/截屏2020-02-26下午11.26.30.png)

### 数据导出

在 1Password 左侧边栏选中一个保险库，点击菜单栏的「文件」-「导出」-「所有项目」，输入主密码验证，1Password
就会将所有账号信息打包成明文文件，供你使用。目前支持3种格式：

  * 1Password 专用文件格式：.1pif 
  * 逗号分隔的文本：.csv 
  * 制表符分隔的文本：.txt 

需要格外注意，导出的文件是未加密的明文，任何人拿到这个文件就等于获得里面包含的全部信息，所以务必小心。除非你非常清楚自己在做什么，否则不要轻易导出数据。

![](https://yishi.io/wp-content/uploads/2020/03/image-3.png)

### 加密文件

在[安全上网指南](https://yishi.io/safe-internet-surfing-and-protect-your-
privacy/)这篇文章中，我曾说不要在手机相册中保存敏感照片，如护照信息页、身份证正反面、信用卡等。这是因为我们很容易把手机相册的访问权限授权给第三方应用，而我们不能确保这些应用恪守规范，不随意上传我们的照片。1Password
恰好支持加密文件，这无疑给了这些敏感照片一个容身之地。

在 1Password 点击”+”号，选择「加密文档」，就可以把你想要加密的文件丢进去了。 **1Password 支持 1GB
的文档存储空间，几乎不限制格式，图片、PDF、视频 … 任何你能想到的格式都可以。**

把敏感照片存在随身设备里的好处显而易见。有时候你出国在外，需要用护照信息，但出于安全考虑最好不要随身携带原件以免丢失。
**这时候电子版的护照信息页就能派上用场，上面的护照编号、起止有效期、签证信息等，都可以随手掏出使用，且不用担心这些敏感信息被黑客窃取。**
身份证、驾照等也是同理。

1Password 还支持文件关联功能。假设有3份文件 A、B、C
都是关于同一事件，但出于某种原因你不能将它们合成一份文件，因此只能分别加密。再加上如果平时的命名习惯不好、加密文件过多，文件找起来就非常不方便。

这时文件关联功能就派上用场了，你可以在创建或编辑加密文档时，选择「链接现有文档」或者直接以关联方式添加新的加密文件，
**这样当你查看详情时，1Password 会贴心的将所有与之关联的文件都显示在页面中，供你查阅** 。

### 一些需要注意的设置项

在「偏好设置」- 「安全」中，你会发现 1Password 会定时清除剪贴板的内容，这是因为每次你复制粘贴时，一些敏感信息会留在系统剪贴板上，
**如果不慎被第三方软件（如某狗，某度等厂商的输入法）上传，有可能造成损失** 。你可以调整清除剪贴板的间隔时间，默认是90秒。

![](https://yishi.io/wp-content/uploads/2020/03/image-7.png)

在「偏好设置」-「暸望塔」中，1Password 默认会追踪已保存的网站中是否存在安全漏洞，如果有，1Password
会提醒你尽快修改对应网站的密码。下方还有「检查易受攻击的密码」选项，这其实是调用
[haveibeenpwned](https://haveibeenpwned.com/) 的服务，看你的账号密码是不是在已经在社工库中了，
**如果有，你应该立刻停用这个密码，并修改将所有曾使用过这个密码的账号** 。

![](https://yishi.io/wp-content/uploads/2020/03/image-14.png)

在「偏好设置」-「账户」中，你可以给自己的 1Password 也设置一个双重验证，使用 Authy，Google
Authenticator，甚至硬件形式的 Yubikey 都可以。一旦设置完成， **新设备如果要登录你的 1Password
账号，除了需要用户名、主密码、Secret key之外，还需要你在旧设备上进行额外的确认，多了一重保障** 。

![](https://yishi.io/wp-content/uploads/2020/03/image-9.png)

如果你有朋友也使用 1Password，那么分享账号就变得异常容易。在账号的详情页点击「分享」，就可以邮件、信息、打印、Airdrop（限 Apple
设备）形式把账号发送给朋友。示例便是以 iMessage 形式将账号分享出去，你可以清楚的看到这一长串链接的开头是
"onepassword://"，其他用户只要安装了 1Password，就可以通过链接自动保存其中的账号信息。  

![](https://yishi.io/wp-content/uploads/2020/03/image-10.png)

**以上就是 1Password 简明教程的全部内容，[祝你1Password
使用愉快。](https://www.tkqlhce.com/click-9258661-13433658?url=https%3A%2F%2F1password.com%2Fzh-
cn%2F)**

参考：  
  
BGR - Exclusive: Apple to deploy 1Password to all 123,000 employees,
acquisition talks underway  
1Password - Security and privacy  
1Password - Heartbleed: Imagine no SSL encryption, it’s scary if you try
1Password - Use Watchtower to find passwords you need to change OpenSSL - The
Heartbleed Bug  
Darthnull - 1Password Wrapping up with a few quick topics

4.7 6 votes

文章评分

[1Password](https://yishi.io/tag/1password/)[保护账号](https://yishi.io/tag/%e4%bf%9d%e6%8a%a4%e8%b4%a6%e5%8f%b7/)[加密](https://yishi.io/tag/%e5%8a%a0%e5%af%86/)
