---
title: OpenWRT刷回小米路由器R3P官方固件
description: ''
date: 'Sat Jan 15 2022 09:37:11 GMT+0800 (中国标准时间)'
dateFormatted: 'Sat Jan 15 2022 09:37:11 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
1、从小米下载开发固件，并将其重命名为miwifi.bin放到U盘(FAT/FAT32)根目录。
2、打开WINSCP，上传kernel0.bin到路由器/tmp目录下。
   然后SSH连接到路由器输入
```
cd /tmp
mtd write kernel0.bin kernel
```
3、拔掉电源将U盘插到路由器。
4、重新插入电源，按住复位键等待黄灯闪烁再松开复位键,等待5分钟安装固件。

文件下载：
https://cyr580.github.io/c/kernel0.bin
https://cyr580.github.io/c/miwifi.bin
