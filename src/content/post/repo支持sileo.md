---
title: repo支持sileo
description: ''
date: 'Fri Apr 02 2021 22:10:30 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Apr 02 2021 22:10:30 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

![](https://i.loli.net/2021/04/02/Z3P8pLryEvqAunm.png)

比较简单，只需增加json
<!-- more -->

# 结构
* repo.xx.com（源地址根目录）
  * sileo（json目录）
    * assets（图片目录）  


## 模版
[点击下载](https://www.dropbox.com/s/ka96wajgsynndcp/sileo%E6%94%AF%E6%8C%81%E6%A8%A1%E7%89%88.zip?dl=0)  
## cydia/zebra与sileo网页描述，分别需要添加json，在deb插件描述文件内添加以下内容  



```HTML
Depiction: https://evynw.github.io/depictions/?p=com.cyr580.xigua31.SB
SileoDepiction: https://cyr580.github.io/sileo/xigua31.SB.json
```
