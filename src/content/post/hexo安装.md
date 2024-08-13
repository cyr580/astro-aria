---
title: hexo安装
description: ''
date: 'Tue Mar 30 2021 01:10:30 GMT+0800 (中国标准时间)'
dateFormatted: 'Tue Mar 30 2021 01:10:30 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

![](https://i.loli.net/2021/03/29/rRUQFn7BfKNyYmk.jpg)

# 安装 Hexo

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。
<!-- more -->
<br>

    ```
npm install -g hexo-cli
```
<br>

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。<br>

    ```
hexo init <folder>
cd <folder>
npm install
```
<br>

文件结构
<br>

    
    ```.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
<br>


    ```
hexo new page —path about/me ”About me“
hexo new page —path about/me
```
<br>


    ```
cd blog  #进入blog目录
hexo cl #清理缓存
hexo g #生成网站文件
hexo s #本地测试代码，Ctrl+c停止本地映射
hexo d #推送本地代码到github
http://localhost:4000
```
<br>

# 补充

    ```
npm install hexo-deployer-git —save
```
