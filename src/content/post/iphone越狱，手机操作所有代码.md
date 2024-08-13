---
title: iPhone越狱，手机操作所有代码
description: ''
date: 'Tue Mar 16 2021 02:30:10 GMT+0800 (中国标准时间)'
dateFormatted: 'Tue Mar 16 2021 02:30:10 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---


![](https://i.loli.net/2021/03/30/mP4R3beIQDSdkua.jpg)
脱离电脑端，iPhone/iPad（ios14）操作jekyll上传文章、修改网站代码等，非常实用  

<!-- more -->
**准备工作**  

1. 手机越狱  
2. 安装插件newterm 2/filza/git  
3. github仓库  


**代码**  


```DOS
su  
alpine  
git clone https://github.com/username/username  
cd /var/mobile/Documents/github/repo  
sudo su - root
git branch master
```

**代码**  


```DOS
git add —all  
git commit -m”blog“  
git push origin master  
git push -u origin master -f
```

**代码**  

```DOS
克隆代码：git clone 远程仓库的url
配置邮箱：git config —global user.email “58054530@qq.com”
配置用户名：git config —global user.name “cyr580”
从远程仓库下拉代码到本地：git pull
放弃本地代码的修改：git checkout — <file>
将本地代码添加到缓冲区：git add * .
移除add到缓冲区的文件：git reset HEAD <file>
将本地代码提交到本地仓库：git commit -m”fp“
将本地仓库同步到远程仓库：git push origin master
查看日志：git log
查看某个文件的提交日志：git log 文件名
查看某个用户的提交日志：git log —author=“author”
查看某条提交日志相信信息：git show 版本号
查看git全部命令：git —help
查看git某个命令的使用：git help 命令名

定位到abc.deb插件所在文件夹，输入cd /var/mobile/aaa 回车
输入解包命令 dpkg-deb -x ./abc.deb ./tmp 回车

输入命令dpkg-deb -e ./abc.deb ./tmp/DEBIAN回车

修改完成退出。执行赋予权限命令以及打包命令

*输入chmod –R 755 ./ tmp/DEBIAN（赋予tmp/DEBIAN文件夹0755命令，否则打包不成功）

🍉 chmod 755 路径

*输入dpkg-deb -b ./tmp false8.deb

git init
echo ”Hello World“ > index.html


Depends: mobilesubstrate, firmware (>= 11.0), com.junesiphone.lockpluspro | com.junesiphone.lockpluspro, com.junesiphone.frontpage | com.junesiphone.frontpage


git config —global user.name ”none“
git config —global user.email ”none@gmail.com“

git config user.email ”58054530@qq.com“

git config user.name ”cyr580“


git config -l


git仓库删除所有提交历史记录，成为一个干净的新仓库
APRIL 28TH, 2017

把旧项目提交到Git上，但是会有一些历史记录，这些历史记录中可能会有项目密码等敏感信息。如何删除这些历史记录，形成一个全新的仓库，并且保持代码不变呢？
1.Checkout

   git checkout —orphan latest_branch

2. Add all the files

   git add -A

3. Commit the changes

   git commit -am ”commit message“


4. Delete the branch

   git branch -D master

5.Rename the current branch to master

   git branch -m master

6.Finally, force update your repository

   git push -f origin master
```

**代码**  

```DOS
apk update
apk upgrade
apk add bash
apk add —no-cache bzip2-dev
apk add —no-cache bash
apk add bash-doc
apk add dpkg-dev
bash ./1.sh
```
