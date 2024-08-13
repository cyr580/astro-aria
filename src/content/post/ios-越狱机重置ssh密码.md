---
title: iOS 越狱机重置ssh密码
description: ''
date: 'Fri Apr 02 2021 05:40:30 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Apr 02 2021 05:40:30 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

![](https://i.loli.net/2021/04/01/wYDScjvZ1tHFKRN.jpg)

ios14越狱后ssh/root登录密码忘记了，查资料得知iPhone的账号密码修改方式，下面有详细教程
<!-- more -->
### 路径
`/private/etc/master.password`
### 使用filza找到下面行  

```
root:xxxxxxxxxxxxx:0:0::0:0:System Administrator:/var/root:/bin/sh
mobile:xxxxxxxxxxxxx:501:501::0:0:Mobile User:/var/mobile:/bin/sh
```
### 将root:及mobile:后面的13个x字符处修改成  

```
root:/smx7MYTQIi2M:0:0::0:0:System Administrator:/var/root:/bin/sh
mobile:/smx7MYTQIi2M:501:501::0:0:Mobile User:/var/mobile:/bin/sh
```

### 修改后保存此文件，你越狱机的ssh密码就重新回到<font color=#FF0000>默认</font>的：`alpine`
