---
title: 关于ios制作修改deb插件
description: ''
date: 'Fri Apr 02 2021 05:52:30 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Apr 02 2021 05:52:30 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
![](https://i.loli.net/2021/04/01/KC83IhRA4bi7cWV.jpg)

简单易懂的语言来理解deb内文件
<!-- more -->
# 很早想写这篇教程，但是懒...
#### 结构  

+ DEBIAN
    - control  

+ /var （可以是任何文件目录，根据不同插件来决定）
    - /var/mobile/Library/FrontPage/xx/xx

#  首先修改control文件
![](https://i.loli.net/2021/04/01/rW5QLyfp24snwKe.jpg)  


```
Package: 插件包的名称，通常是com.xx.xx
Version: 版本
Section: 类别
Depends: 依赖
Architecture: iphoneos-arm
Name: 插件名
Author: cyr580
Maintainer: 维护者 <cyr580@qq.com>
Description: 描述
Icon: 图标
Depiction: 网页描述
```
# 解包/打包deb📦  
1. 定位到abc.deb插件所在文件夹，输入cd /var/mobile/aaa 回车（aaa代表文件夹路径）
2. 输入解包命令 dpkg-deb -x ./abc.deb ./tmp 回车
3. 输入命令dpkg-deb -e ./abc.deb ./tmp/DEBIAN回车
4. 修改完成退出。执行赋予权限命令以及打包命令，输入chmod –R 755 ./ tmp/DEBIAN（赋予tmp/DEBIAN文件夹0755命令，否则打包不成功），或者chmod 755 路径
5. 输入dpkg-deb -b ./tmp false8.deb
  
  
# <font color=#FF0000>越狱后filza直接解包打包</font>
1. 打开`filza`
2. 找到需要修改的`deb`，比如`a.deb`
3. 点击打开a.deb（不要安装，点击解压）
4. 按照上述教程修改即可
5. <font color=#FF0000>重点来了：修改完成之后，全部选中DEBIAN文件夹和var文件夹</font>，分享，打包DEB（filza自带打包功能）
6. 接上前一篇文章教程，把deb放到debs目录，`.sh`生成packages和packages.bz2文件，push即可
