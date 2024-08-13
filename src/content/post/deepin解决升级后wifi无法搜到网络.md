---
title: Deepin解决升级后wifi无法搜到网络
description: ''
date: 'Thu Oct 28 2021 22:12:34 GMT+0800 (中国标准时间)'
dateFormatted: 'Thu Oct 28 2021 22:12:34 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

![](https://i.loli.net/2021/10/28/cSARgKZktJP8UDE.jpg)

<!-- more -->

## 内核问题，以下命令修复

1. 首先确保电脑已经连接至有线网络，有可用网络连接
使用以下命令在sources.list里添加debian backports源

```
echo "deb http://deb.debian.org/debian buster-backports main contrib non-free" | sudo tee -a /etc/apt/sources.list
```

2. 然后执行

```
sudo apt update

sudo apt autopurge bcmwl-kernel-source broadcom-sta-*

sudo apt -t buster-backports install broadcom-sta-common broadcom-sta-dkms broadcom-sta-source
```
