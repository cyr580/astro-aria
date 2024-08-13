---
title: ios14未越狱运行hexo-git-nodejs-npm
description: ''
date: 'Wed Mar 31 2021 18:35:30 GMT+0800 (中国标准时间)'
dateFormatted: 'Wed Mar 31 2021 18:35:30 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

![](https://i.loli.net/2021/03/31/9OgFDZqEdW4nuYI.jpg)

如果你是一名学习计算机相关专业的学生，或是经常跟Linux打交道的用户，那么Linux必定是你一生挚友。
<!-- more -->
虽然Linux不像微软的桌面系统那样，占据市场的大半江山，但是Linux的开源、免费、稳定和丰富吸引着越来越多用户与之相拥。

自从接触了Linux，我就成了Linux系统的忠实用户，我使用过许多种发行版，也各有各的特色。除了有些没法在Linux上运行的软件会使用Windows，大部分情况都是用Linux。

我不仅在电脑上使用Linux，也会在手机、iPad上使用。在知道iSH前，我在iPad使用Linux都是借助服务器。其实iPad越狱也可以使用Linux Shell，但是为了平板的安全和稳定，也就没越狱，也不提倡。

### 什么是iSH？

iSH其实是一款APP，但是目前还没有在Apple Store正式上线。iSH是一个模拟器，用来在ARM架构的iOS设备上模拟x86架构，让iOS设备在本地运行Linux Shell环境。


![](https://i.loli.net/2021/03/31/mTk14nZ5eJvQPz2.jpg)

这意味着你不用越狱，就可以在一台iOS设备上运行一个Linux系统。我想这是iOS用户的一个福音，而我正是有这个需求的用户。

Alpine Linux是一个由社区开发的Linux操作系统，该操作系统以安全为理念，面向x86路由器、防火墙、虚拟专用网、IP电话盒及服务器而设计。

##### Alpine Linux的特点：

1. 小巧：基于Musl libc和busybox，和busybox一样小巧，非常适合用作Docker镜像。

2. 安全：面向安全的轻量发行版；

3. 简单：提供APK包管理工具，软件的搜索、安装、删除、升级都非常方便。

也许就是这些特点，iSH选用Alpine Linux。

##### （App Store版已正式上线，可直接在应用商店搜索安装）

##### 更换源：

因为Alpine Linux默认使用的是国外的源，使用国外的服务器，网速特别慢，更换成国内阿里云、中科大、清华的源都可以。


```  
vi /etc/apk/repositories
```
在最上面添加这两行：


```  
# 阿里云源
https://mirrors.aliyun.com/alpine/v3.11/main
https://mirrors.aliyun.com/alpine/v3.11/community
# 中科大源
https://mirrors.ustc.edu.cn/alpine/v3.11/main
https://mirrors.ustc.edu.cn/alpine/v3.11/community
```
##### 更新源  


```  
apk update
```

安装一些常用的软件：

zsh：我使用的shell

git：代码版本控制软件，clone我在GitHub上的配置文件

curl：克隆GitHub代码要用到

neofetch：显示当前系统的一些信息

neovim：我最常用的代码编辑器

nodejs：hexo需要用到

npm：hexo需要用到

hexo：必装

```  
apk add zsh git neofetch curl neovim
```
##### 如果没有预装apk，输入以下代码

```  
wget -qO- http://dl-cdn.alpinelinux.org/alpine/v3.12/main/x86/apk-tools-static-2.10.5-r1.apk | tar -xz sbin/apk.static && ./sbin/apk.static add apk-tools && rm sbin/apk.static
# For the latest apk-tools, go to http://dl-cdn.alpinelinux.org/alpine/latest-stable/main/x86/
```
