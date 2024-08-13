---
title: 越狱后修改root密码
description: ''
date: 'Tue Mar 30 2021 00:30:10 GMT+0800 (中国标准时间)'
dateFormatted: 'Tue Mar 30 2021 00:30:10 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---


![](https://i.loli.net/2021/03/29/6lLXi4UDRS3v7GY.jpg)

1:越狱后在CYDIA下载`NewTerm 2`插件，安装好了会要求注销手机
<!-- more -->
2:安装好了桌面点击`NewTerm` 图标，输入  
``` su```  
然后点键盘上的换行键（自带键盘是Return键，第三方键盘是回车键或换行键，建议自带键盘操作），此时会提示输入password，输入默认的密码：
```alpine```  
自己确定输入正确后再点Return键

3.输入正确的原始密码后再输入：
```passwd root```  
此时会提示要求你输入新的密码，输入完自己的密码后按return键，此时会提示再次输入，再输入一次自己的密码，如果两次输入的密码不一样就会提示要求你再次输入new passwd.
