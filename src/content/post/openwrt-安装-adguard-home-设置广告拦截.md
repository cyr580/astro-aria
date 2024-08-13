---
title: OpenWrt 安装 AdGuard Home 设置广告拦截
description: ''
date: 'Fri Jan 14 2022 05:16:53 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Jan 14 2022 05:16:53 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
 AdGuard Home 是广告拦截与反跟踪软件，可以将广告与追踪相关的域名屏蔽，同时不再需要安装任何客户端，包括 Windows、Mac、Android、iOS，下面我们说的是 OpenWrt 安装 AdGuard Home 设置全局广告拦截，教程开始之前，我先介绍一下 AdGuard Home 的工作原理。
<!-- more -->
AdGuard Home 的工作原理是在 DNS 的域名解析过程中拦截网页上的广告，目前支持 DNS over TLS 和 DNS over HTTPS，本教程讲解讲解如何配置 OpenWRT 的 AdGuardHome 实现DNS防污染加快网站解析速度 和 广告拦截。

![](https://s2.loli.net/2022/01/13/4JygMN3zUbjTAVH.jpg)


## 插件下载
AdGuard Home[⏬点击下载](https://cloud.opssh.cn/chajian/luci-app-adguardhome_1.8-11_all.ipk)

AdGuard Home源码[⏬点击下载源码](https://github.com/cyr580/luci-app-adguardhome)

## 插件安装
方法一

通过本站高速下载好 AdGuard Home 插件，打开 OpenWrt 管理界面，进入系统列表页找到文件传输，选择上传 AdGuard Home 插件，并在上传文件列表进行安装，如下图：
![](https://s2.loli.net/2022/01/13/R7lJwkNpu83nChZ.jpg)
方法二

打开 OpenWrt 管理界面，进入系统列表页找到软件包，将 本站的 AdGuard Home 插件高速下载网址 复制到 下载并安装软件包的填写框内，点击确定，如下图：
![](https://s2.loli.net/2022/01/13/toEPQrC8DFkK3Hn.jpg)

## 使用教程
1、点击 服务 -> AdGuard Home，更新核心版本，等待核心更新完成并启用 AdguardHome 插件，点击日志，如果有运行记录，则表示AdGuardHome已正常运行，如下图：
![](https://s2.loli.net/2022/01/13/DOAWUyfebiXRzxk.jpg)
2、置 AdGuardHome 密码，点击 改变网页登录密码 并添加，填写 改变网页登录密码，点击载入计算模块，然后再点击计算，如下图：
![](https://s2.loli.net/2022/01/13/SjZgVmziGp7UD8v.jpg)
3、点击按钮进入 AdGuardHome，或在地址栏中输入 192.168.2.1:3000，进入后配置 AdGuardHome，注意：账号为 root，密码为上一步你设置的密码，比如我的：admin，如下图：

注意：配置 AdGuardHome 时，设置端口环节，建议手动修改，比如默认80，53，我就修改成了8080，55
![](https://s2.loli.net/2022/01/13/2pchMYH4iNQsxl5.jpg)
4、进入 AdGuardHome 控制台后，点击 设置 进入 DNS设置，如下图：
![](https://s2.loli.net/2022/01/13/PfS6VCGvDq3MLly.jpg)
5、进入 DNS设置 后，填写 上游 DNS 服务器，选择 并行请求，填写 Bootstrap DNS 服务器，上游 DNS 服务器 和 Bootstrap DNS 服务器已经列举在下面了，如下图：
![](https://s2.loli.net/2022/01/13/3dzFhSNofcexiBY.jpg)
特别注意：Bootstrap DNS 用于解析上游DNS，所以尽可能将 Bootstrap DNS 的第一条设置为当地运营商的DNS地址（支持IPV6），当地运营商的DNS地址可通过直接命令框内使用 ipconfig /all 查询，前提是必须网线直接插在光猫上

上游 DNS 服务器
```
114.114.114.114
114.114.115.115
223.5.5.5
223.6.6.6
119.29.29.29
180.76.76.76
101.226.4.6
123.125.81.6
101.226.4.6
101.226.4.6
https://dns.google/dns-query
https://dns.quad9.net/dns-query
https://doh.opendns.com/dns-query
https://1.1.1.1/dns-query
tls://dns.rubyfish.cn
tls://8.8.8.8
tls://8.8.4.4
tls://dns.google:853
```

Bootstrap DNS 服务器
```
当地电信DNS
当地移动DNS
当地联通DNS
119.29.29.29
223.5.5.5
180.76.76.76
8.8.8.8
8.8.4.4
208.67.222.222
```

6、点击 过滤器 ，选择 DNS封锁清单，添加下方合适的规则并将对应规则打钩，软后点击检查更新，如下图：
![](https://s2.loli.net/2022/01/13/8FpCOVgtouD9GyX.jpg)
7、返回 OpenWrt 的 AdGuard Home 插件设置内将重定向设置为 作为dnsmasq 的上游服务器即可，这样我就让 AdGuardHome 生效了，如下图：
![](https://s2.loli.net/2022/01/13/krGQE3iBvgoOz8e.jpg)
## 注意事项
前面就是全部的教程内容了，拦截效果由规则决定，建议使用合适的规则，不要滥用规则，拦截效果可到 AdGuard Home 网页管理内查看。

网络环境中，多个DNS缓存可能造成网络访问异常，所以需要进入 AdGuard Home 网页管理处，点击 设置，选择 DNS设置，将DNS缓存大小设置为 0 即可
