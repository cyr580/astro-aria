---
title: 国内外免费公共 DNS 服务推荐
description: ''
date: 'Sat Jan 15 2022 19:29:37 GMT+0800 (中国标准时间)'
dateFormatted: 'Sat Jan 15 2022 19:29:37 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
![](https://s2.loli.net/2022/01/15/y4XoUTxJkCPj9mG.jpg)
<!-- More --> 
我们都知道想要能上网，就必须要使用DNS。DNS一般都是你的运营商提供给你的，也可以是一些其它组织提供的，比如我们熟知的谷歌的DNS 8.8.8.8，国内114dns的114.114.114.114 。这些由大的厂商和机构提供的公开解析服务，叫做公共DNS。

不过首先要明白，公共DNS不是：

-   不是根服务器
-   不是权威dns托管商，不提供域名注册等服务，比如万网和DNSpod
-   不是权威dns，不针对个别域名进行解析

公共DNS服务的特点就是服务的域名数量巨大，用户数多，同时要求具有安全性和抗攻击性，低延迟（响应快），无拦截（无广告）以及对解析成功率要求非常的高。并在一定程度上提高网页的链接速度，因此选择使用一个优秀的DNS，可以显著的提高网络冲浪体验。

下面微观君就介绍一些国内外优秀的公共DNS供大家选用。

* * *

国内公共 DNS
--------

**腾讯云 DNS**
-----------

Public DNS+ 是 DNSPod 推出的公共域名解析服务，DNSPod 曾是中国第一大DNS解析服务提供商，现在 DNSPod 已经被腾讯云收购，因此也叫做腾讯公共 DNS 服务。腾讯 DNS 可以为用户提供更加快速、准确、稳定的递归解析服务，且不会对任何域名进行恶意劫持。

```text
IPv4 DNS 地址：119.29.29.29
```

服务地址：[https://www.dnspod.cn/Products/Public.DNS](https://link.zhihu.com/?target=https%3A//www.dnspod.cn/Products/Public.DNS)

阿里云公共 DNS
---------

由阿里云提供的公共DNS服务。阿里云拥有全球数百台服务器组成的集群，具有充足的带宽资源；其自研高性能DNS系统和清洗中心，保障系统稳定和安全。BGP anycast技术，让您访问最近的DNS集群；动态缓存技术，加速解析响应。阿里云公共 DNS具有稳定，快速，智能的优势。

```text
IPv4 DNS 地址：223.5.5.5 / 223.6.6.6
IPv6 DNS 地址：2400:3200::1 / 2400:3200:baba::1
```

服务地址：[https://alidns.com/](https://link.zhihu.com/?target=https%3A//alidns.com/)

**百度公共 DNS**
------------

由百度推出的公共DNS的服务，依托百度强大技术，具有云防护，无劫持，更精准三大优势。

-   云防护：病毒、木马、钓鱼网站一网拦截，百度云防护实时守护您的访问安全
-   无劫持：无恶意跳转，无强制广告，百度公共DNS让您的每一次访问都畅通无阻
-   更精准：遍布全国的递归出口、智能解析，所有的努力只为让CDN定位更精准，让您的每一次访问都更高效

  

```text
IPv4 DNS 地址：180.76.76.76
IPv6 DNS 地址：2400:da00::6666
```

服务地址：[https://dudns.baidu.com/intro/publicdns](https://link.zhihu.com/?target=https%3A//dudns.baidu.com/intro/publicdns)

**114 DNS**
-----------

114 DNS 源自南京信风 2010 年为中国电信及中国联通两个大省约 2000 万宽带用户提供备份服务的超大型 DNS 系统，同时提供公众 DNS 解析服务及权威 DNS 解析备份服务，114DNS 将为中国的互联网及电子商务提供可靠的基础安全保障。114DNS 为国内云安全DNS服务先行者，114DNS 平台由多个基础电信运营商与南京信风共建共享，但由南京信风提供技术支持以确保服务的优质高效。

```text
IPv4 DNS 地址：114.114.114.114 / 114.114.115.115
```

服务地址：[http://www.114dns.com/](https://link.zhihu.com/?target=http%3A//www.114dns.com/)

**OneDNS**
----------

OneDNS是北京微步在线科技有限公司旗下产品，为防止DNS解析服务被滥用，OneDNS个人版对来自每个IP地址的解析请求量做了限制，其解析服务分为拦截版，纯净版，家庭版三种。拦截版含有恶意网站拦截、广告过滤等功能；纯净版则不对访问网站进行任何过滤拦截，直接返回其真实的响应结果。

```text
拦截版 IPv4 DNS 地址：117.50.11.11    52.80.66.66
纯净版 IPv4 DNS 地址：117.50.10.10    52.80.52.52
家庭版 IPv4 DNS 地址：117.50.60.30    52.80.60.30
```

服务地址：[https://www.onedns.net](https://link.zhihu.com/?target=https%3A//www.onedns.net)

* * *

国外DNS 服务
--------

**谷歌公共 DNS**
------------

谷是最早推出免费DNS服务的平台。谷歌DNS它们易于记忆，并且每个人都可以使用。谷歌DNS的主要优势来自他们作为一家公司的声誉。谷歌每年收入极多，有能力提供最稳定和更有弹性的DNS服务器。这个DNS服务器的唯一问题是它们存储有关您的运营的信息，如果美国政府决定需要这些信息，它们可以与第三方共享，Google通常被认为是最好的DNS服务器。

```text
IPv4 DNS 地址：8.8.8.8 / 8.8.4.4
```

服务地址：[https://developers.google.com/speed/public-dns](https://link.zhihu.com/?target=https%3A//developers.google.com/speed/public-dns)

**Cloudflare DNS**
------------------

cloudflare 是一家国外的 CDN 加速服务商。2018 年的 4 月 1 日愚人节，Cloudflare 宣布推出 1.1.1.1 公共 DNS 服务。如今两年过去了，其已经成为了仅次于 Google 的全球第二大公共 DNS 解析器。cloudflare DNS目标互联网上速度最快且高度关注隐私保护的消费级 DNS 服务

```text
IPv4 DNS 地址：1.1.1.1 和 1.0.0.1
IPv6 DNS 地址：2606:4700:4700::1111 和 2606:4700:4700::1001
```

服务地址：[https://developers.google.com/speed/public-dns](https://link.zhihu.com/?target=https%3A//developers.google.com/speed/public-dns)

**OpenDNS**
-----------

OpenDNS 是一个免费的域名解析服务提供商（DNS），并具备反钓鱼、内容控制软件等功能。2015年6月30日，思科系统公司宣布收购OpenDNS。OpenDNS为个人和商业提供DNS方案，用户可以自行选择使用OpenDNS的服务或者使用当地ISP提供的DNS服务。

```text
IPv4 DNS 地址：208.67.222.222 / 208.67.220.220
IPv4 DNS 地址：208.67.222.220 / 208.67.220.222
IPv6 DNS 地址：2620:119:35::35 / 2620:119:53::53
```

服务地址：[https://www.opendns.com/](https://link.zhihu.com/?target=https%3A//www.opendns.com/)

  

总结：对于国内用户微观君推荐大家使用腾讯云 阿里云的公共 DNS，作为云服务器大厂，公共DNS算是基础服务，势必有不错的保证。国外用户选Cloudflare的公共DNS服务，在速度和隐私方面都做的很好。
