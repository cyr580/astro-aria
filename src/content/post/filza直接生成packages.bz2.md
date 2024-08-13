---
title: Filza直接生成packages.bz2
description: ''
date: 'Fri Apr 02 2021 22:40:30 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Apr 02 2021 22:40:30 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
-
由于ios无dpkg-scanpackages命令，无奈google，终于找到了几年前WF一位网友分享的sh，可以在手机上直接生成packages.bz2
-
<!-- more -->
> 环境：任何支持dpkg命令的unix系统
> 工具：dpkg及相关组件

* iPhone OS（已越狱）：自带dpkg-deb命令，无dpkg-scanpackages命令
* Debian/Ubuntu：自带dpkg-deb和dpkg-scanpackages命令
* Fedora: 无dpkg相关命令
* Mac OS X：无任何dpkg相关命令
* Windows：非unix系统，无dpkg相关命令 以上系统中，Fedora不支持dpkg，也无法通过安装系统组件来支持dpkg，因此Fedora系统不能用于生成Packages文件。
而对于Mac OS X系统，本身虽然不支持dpkg，但可以通过安装一个叫 Fink 的软件来获得dpkg命令。
Fink 下载页面： http://www.finkproject.org/download/
如何安装请见官网说明。
对于Windows系统，可以通过安装 Cygwin + dpkg 来获取dpkg命令。
Cygwin下载地址： http://www.cygwin.com/setup.exe
dpkg命令可以直接在Cygwin中获取。
但个人不推荐在Windows下使用dpkg，因为Cygwin体积很大，与其安装这个，还不如直接安装个Ubuntu来的简单。
各个系统下生成Packages的方法基本一样。
最简单的方法是利用dpkg-scanpackages命令来制作Packages文件。
iPhone OS 不适用（因为没有这个命令）


-------
1. 手机打开filza
2. 将需要发布的deb文件放在debs目录
3. cd repo根目录
4. sh文件与debs文件夹同级
5. 执行命令（下面的sh）


[<font color=#FF0000>点击下载sh</font>](https://www.dropbox.com/s/dp2nme0mbii3tqi/Filza-update.sh?dl=0)  
