---
title: 越狱手机上直接搭建cydia-repo源（github）
description: ''
date: 'Thu Apr 01 2021 22:57:30 GMT+0800 (中国标准时间)'
dateFormatted: 'Thu Apr 01 2021 22:57:30 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

![](https://i.loli.net/2021/04/01/qEky7oj31FriUm8.jpg)

拥有一个自己的repo，越狱后，各种折腾美化、插件，闲得蛋疼可以试试自己搭建一个repo，搭建容易，维护不易，需要花大量时间来关注并更新！
<!-- more -->

# 准备工作

1. git  ——默认Boss源或者[点击直达procurs-Taurine](https://apt.procurs.us/)
2. newterm2  ——[点击直达packix](https://repo.packix.com/)
3. github仓库  ——[点击直达github](https://www.github.com)
4. Filza  ——[点击直达akemi](https://cydia.akemi.ai/)

# 创建github仓库

![](https://i.loli.net/2021/04/01/HZfdW1j93JTtlnI.jpg)
![](https://i.loli.net/2021/04/01/USI6GrwRO15DEzs.jpg)

#### 复制下面这个地址（后面需要推送到这里）

![](https://i.loli.net/2021/04/01/2AjUqt97QfuOeBi.jpg)

# 手机newterm把这个仓库克隆到本地

1. 打开newterm
2. 输入`su`<font color=#FF0000>必须获取root权限</font>
3. 输入`alpine`(默认root密码)
4. 打开filza，我在Document目录下创建一个github文件夹
5. `cd /var/mobile/Documents/github/`我的文件夹路径
6. `git clone https://github.com/cyr580/myrepo`我的仓库地址
7. 打开filza，找到/Documents/github/myrepo
8. 把我传的文件复制进myrepo文件夹根目录[点击下载文件](https://www.dropbox.com/s/laqs0fsfjoneg7b/myrepo.zip?dl=0)  


#### 接着修改各种文件 
—Release文件  
![](https://i.loli.net/2021/04/01/5z4XQPLDNwKZfRq.jpg)
—deb插件放入/debs目录

#### 接着自动生成packages和packages.bz2文件
这个是源列表文件，有了这个文件才可以在cydia搜索到你的插件
上面发的文件内有一个`xxxx.sh`的文件，<font color=#FF0000>手机打开Filza点击sh文件，运行即可</font>
检查目录下packages文件是否为0kb（0kb肯定有问题），如果你添加了deb到debs文件夹，那这个列表生成后会占用空间，而不是0kb

# 最后就是git推送到仓库和更改github pages分支

1. 打开newterm
2. `su`
3. `alpine`默认密码
4. `cd /var/mobile/Documents/github/myrepo`，看清楚🧐，cd到的目录是myrepo
5. `git add -A`添加全部文件
6. `git commit -m"repo"`，日志，每次必须操作一次，后面的repo字母可以随意改英文或者数字
7. `git push origin master`，推送到仓库，这里会踩坑，文章最后会说到
8. `git branch master`<font color=#FF0000>创建分支，下面github pages改为master分支，保存</font>

![](https://i.loli.net/2021/04/01/OdkylnCSVqAZLmY.jpg)

![](https://i.loli.net/2021/04/01/DBd42C6iOfWnemE.jpg)

# 踩坑

##### 不能git push的原因是没有设置邮箱和名字，输入以下命令  

```Bash  
git config --global user.email “58054530@qq.com”
git config --global user.name “cyr580”
```
##### 每一次增加/删除/修改任何deb文件后，必须点击 `update.sh` 重新生成一次packages/packages.bz2（这是源列表）

![](https://i.loli.net/2021/04/01/jEnRclSVmZp6KN3.jpg)

##### 最后来一次完整的git  


```Bash
#获取root权限
su
#输入密码，下面是默认密码
alpine
#cd 源目录
cd /xx/xx/xx/xx
#添加deb到debs，并用.sh文件生成packages和packages.bz2，接着git
git add -A
#日志，每次必须操作
git commit -m“repo”
#推送到仓库
git push
#输入github的登录帐号和密码
xxxxx 回车
xxxxx 回车
等待推送，会跑命令...
接着去添加源愉快的玩耍吧
```
