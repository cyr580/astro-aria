---
title: NanoPi-R2S刷系统
description: ''
date: 'Tue Aug 16 2022 23:41:38 GMT+0800 (中国标准时间)'
dateFormatted: 'Tue Aug 16 2022 23:41:38 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
![r2s](https://github.com/cyr580/blog-comment/blob/main/IMG_1681.JPG?raw=true)

## 准备工作
- win32diskimager
- SD卡
------
## 详细步骤
- 准备一张8G或以上容量的TF卡
- 下载并解压镜像文件 xxx.img.gz 和工具 win32diskimager
- 在Windows下以管理员身份运行 win32diskimager
- 在界面上选择你的SD卡盘符
- 选择解压后的固件文件
- 点击 Write 按钮烧写到SD卡
- 或者在 Linux下使用 dd 命令将 xxx.img 写入 SD卡
- 将SD卡从电脑端弹出，插入NanoPi-R2S的microSD卡槽
- 连接NanoPi-R2S的电源，系统会从TF卡启动
------
## 固件下载地址和wiki
- https://github.com/DHDAXCW/NanoPi-R2S-rk3328/releases/download/2022.08.12-Lean1/openwrt-rockchip-armv8-friendlyarm_nanopi-r2s-squashfs-sysupgrade.img.gz
- https://github.com/DHDAXCW/NanoPi-R2S-rk3328/releases
- https://wiki.friendlyelec.com/wiki/index.php/NanoPi_R2S/zh
