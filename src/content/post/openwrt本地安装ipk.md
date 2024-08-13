---
title: openwrt本地安装ipk
description: ''
date: 'Fri Jan 14 2022 05:06:40 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Jan 14 2022 05:06:40 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# 0penwrt固件离线安装IPK插件教程
（以WIN系统为例）

当我们不想换系统，而只想安装一个里面没有的插件时，可以试试OpenWrt固件离线安装IPK插件教程。废话不多说，开整。
<!-- more -->
准备工作：
	1. 电脑上安装好winscp这个软件（自行百度下载安装）以及要安装的ipk插件保存到电脑上。
	2. 用网线或者无线连接你的路由器，保证能进入到路由器的系统界面，路由器的ssh要开启（openwrt固件基本上默认都是开启的）
	3. 打开winscp工具：

![图片](/assets/o1.jpg)

备用说明图 输入命令<font color=green>opkg install xxxx.ipk</font>
