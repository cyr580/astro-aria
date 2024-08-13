---
title: 转载：小雅全家桶来啦，小白用户群晖部署 Emby 简明教程
description: ''
date: 'Fri Feb 16 2024 00:00:08 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Feb 16 2024 00:00:08 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# 转载：小雅全家桶来啦，小白用户群晖部署 Emby 简明教程

**前言：**

为什么要出这个教程？

在我写上一篇教程的时候，小雅已经更新了全家桶。经网友提醒，本次及时补上教程。鉴于网上有许多大神已经出了教程，本教程注重实操，对于像我这样的小白用户来说，简单无脑操作、能快速部署才是关键。

**安装全家桶有什么作用？**

因为小雅网盘挂载到本地但是 Emby 无法搜刮，本次全家桶将网盘上百T的影视资源进行整理搜刮部署到本地，实现 Emby 海报墙，优雅地看电影。

**使用环境：**

PVE、Unraid、ESXi、物理群晖、N1盒子都可以部署，安装需要160G以上硬盘空间也可以使用外接硬盘（U盘），本人使用PVE安装的群晖7.2。

*本教程适用于群晖下部署*

**正篇：**

为了确保安全顺利，请大家提前将群晖已安装的 Emby、小雅网盘容器先删除并清空群晖 Docker文件夹，跟着教程一步一步部署。不想删除原有 Emby 可以将8096端口改为8097。

**一、本地部署小雅网盘**

可以参考该教程：[https://post.smzdm.com/p/a0qnlpqw/](https://post.smzdm.com/p/a0qnlpqw/)

1. 在群晖下新建文件夹xiaoya（添加everyone读写权限）

`/volume1/docker/xiaoya`

2. 获取阿里云`mytoken.txt`、`myopentoken.txt`、`temp_transfer_folder_id.txt`

    - `mytoken.txt`（推荐使用手机端）

        安卓：[https://luoflower.com/128/](https://luoflower.com/128/)

        苹果：[https://aliyuntoken.vercel.app/](https://aliyuntoken.vercel.app/)

        电脑：[https://alist.nn.ci/zh/guide/drivers/aliyundrive.html](https://alist.nn.ci/zh/guide/drivers/aliyundrive.html)

    - `myopentoken.txt`

        [https://alist.nn.ci/tool/aliyundrive/request](https://alist.nn.ci/tool/aliyundrive/request)

    - `temp_transfer_folder_id.txt` 

        登陆阿里云盘[https://www.aliyundrive.com/drive](https://www.aliyundrive.com/drive)，在资源盘下新建文件夹（xiaoya），点击进入后复制阿里云盘转存目录 folder id 填入 `temp_transfer_folder_id.txt`

3. 将以上获取的密钥分别填入新建文本 `mytoken.txt`、`myopentoken.txt`、`temp_transfer_folder_id.txt`，上传至群晖 `docker/xiaoya` 文件夹中。

4. 使用ssh登陆群晖 `sudo -i` 登陆root账号使用以下命令

    ```bash
    docker run -d --restart=always --name="xiaoya" -p 5678:80 -p 2345:2345 -p 2346:2346 -v /volume1/docker/xiaoya:/data xiaoyaliu/alist:latest
    ```

5. 在群晖 Docker下启动 `xiaoya` 容器，浏览器打开 `http://群晖ip地址:5678/`，需等5分钟左右刷新浏览器验证是否挂载成功。

6. 实时清理自己阿里盘缓存命令安装 `xiaoyaleep`

    ```bash
    bash -c "$(curl -s https://xiaoyahelper.zngle.cf/aliyun_clear.sh | tail -n +2)" -s 3 -tg
    ```

    每24h自动清除缓存在自己阿里云下小雅缓存。上面这个命令后缀 `-tg` 可以删除，这个是电报机器人接收通知。

**二、挂载 Emby 全家桶**

**准备工作：**

1. 在 `/volume1/docker/xiaoya` 下新建两个文本文档

    - `docker_address.txt`，填写 `http://群晖ip地址:5678`（注意内容格式，没有/，本人就是因为格式问题导致部署失败浪费了大量时间）
    - `emby_server.txt`，填写 `http://群晖ip地址:8096`
    
2. 在 `/volume1/docker/xiaoya` 下新建文件夹 `media`（添加everyone读写权限）

3. 登陆本地小雅网盘，`http://群晖ip地址:5678`，任意打开一个mp4视频，验证是否正常播放。出现“Failed to refresh token: Too Many Requests”说明刷新令牌次数过多需要关闭 `xiaoya` 容器等待1小时。

**部署命令：**

使用ssh登陆群晖 `sudo -i` 登陆root账号使用以下命令

*二选一*

- 使用 Emby 官方容器命令（无法调用核显硬解）

    ```bash
    bash -c "$(curl http://docker.xiaoya.pro/emby_plus.sh)" -s /volume1/docker/xiaoya/media   /volume1/docker/xiaoya
    ```

- （推荐）使用第三方 Emby 容器命令，（可以调用核显硬解）

    ```bash
    bash -c "$(curl http://docker.xiaoya.pro/emby_plus.sh | sed 's#emby/embyserver#amilys/embyserver#')" -s /volume1/docker/xiaoya/media   /volume1/docker/xiaoya
    ```

调用核显需要高级权限，在群晖 Container Manager 找到 Emby 容器，停用后打开“使用高级权限”选项。

下载缓存时间较长，需要1~2小时甚至更长，根据网络和NAS性能，完成后会有提示请耐心等待，完成后重启 `xiaoya` 容器，使用官方 Emby 推荐使用2345端口号登陆 Emby“`http://群晖:2345`，用客户端进行硬解，使用第三方 Emby 2345、8096端口都可以使用。

**结尾：**

大家在部署过程中遇到问题，本人小白能力有限，可以去小雅网站查找或者官群里咨询，本教程注重的是实操，小雅美女不辞辛苦为大家谋福利每天修改BUG搜刮海报付出了大量心血，请大家尊重小雅劳动果实，打赏作者为知识付费。小雅还在不断进化请大家保持关注，小雅官网地址：[alist.xiaoya.pro](alist.xiaoya.pro)。

作者声明本文无利益相关，欢迎值友理性交流，和谐讨论～
[原文地址-什么值得买](/media%20%20%20/volume1/docker/xiaoya%20%20%20%20%20%60%60%60%20%20%E8%B0%83%E7%94%A8%E6%A0%B8%E6%98%BE%E9%9C%80%E8%A6%81%E9%AB%98%E7%BA%A7%E6%9D%83%E9%99%90%EF%BC%8C%E5%9C%A8%E7%BE%A4%E6%99%96%20Container%20Manager%20%E6%89%BE%E5%88%B0%20Emby%20%E5%AE%B9%E5%99%A8%EF%BC%8C%E5%81%9C%E7%94%A8%E5%90%8E%E6%89%93%E5%BC%80%E2%80%9C%E4%BD%BF%E7%94%A8%E9%AB%98%E7%BA%A7%E6%9D%83%E9%99%90%E2%80%9D%E9%80%89%E9%A1%B9%E3%80%82%20%20%E4%B8%8B%E8%BD%BD%E7%BC%93%E5%AD%98%E6%97%B6%E9%97%B4%E8%BE%83%E9%95%BF%EF%BC%8C%E9%9C%80%E8%A6%811~2%E5%B0%8F%E6%97%B6%E7%94%9A%E8%87%B3%E6%9B%B4%E9%95%BF%EF%BC%8C%E6%A0%B9%E6%8D%AE%E7%BD%91%E7%BB%9C%E5%92%8CNAS%E6%80%A7%E8%83%BD%EF%BC%8C%E5%AE%8C%E6%88%90%E5%90%8E%E4%BC%9A%E6%9C%89%E6%8F%90%E7%A4%BA%E8%AF%B7%E8%80%90%E5%BF%83%E7%AD%89%E5%BE%85%EF%BC%8C%E5%AE%8C%E6%88%90%E5%90%8E%E9%87%8D%E5%90%AF%20%60xiaoya%60%20%E5%AE%B9%E5%99%A8%EF%BC%8C%E4%BD%BF%E7%94%A8%E5%AE%98%E6%96%B9%20Emby%20%E6%8E%A8%E8%8D%90%E4%BD%BF%E7%94%A82345%E7%AB%AF%E5%8F%A3%E5%8F%B7%E7%99%BB%E9%99%86%20Emby%E2%80%9C%60http://%E7%BE%A4%E6%99%96:2345%60%EF%BC%8C%E7%94%A8%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%BF%9B%E8%A1%8C%E7%A1%AC%E8%A7%A3%EF%BC%8C%E4%BD%BF%E7%94%A8%E7%AC%AC%E4%B8%89%E6%96%B9%20Emby%202345%E3%80%818096%E7%AB%AF%E5%8F%A3%E9%83%BD%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8%E3%80%82%20%20**%E7%BB%93%E5%B0%BE%EF%BC%9A**%20%20%E5%A4%A7%E5%AE%B6%E5%9C%A8%E9%83%A8%E7%BD%B2%E8%BF%87%E7%A8%8B%E4%B8%AD%E9%81%87%E5%88%B0%E9%97%AE%E9%A2%98%EF%BC%8C%E6%9C%AC%E4%BA%BA%E5%B0%8F%E7%99%BD%E8%83%BD%E5%8A%9B%E6%9C%89%E9%99%90%EF%BC%8C%E5%8F%AF%E4%BB%A5%E5%8E%BB%E5%B0%8F%E9%9B%85%E7%BD%91%E7%AB%99%E6%9F%A5%E6%89%BE%E6%88%96%E8%80%85%E5%AE%98%E7%BE%A4%E9%87%8C%E5%92%A8%E8%AF%A2%EF%BC%8C%E6%9C%AC%E6%95%99%E7%A8%8B%E6%B3%A8%E9%87%8D%E7%9A%84%E6%98%AF%E5%AE%9E%E6%93%8D%EF%BC%8C%E5%B0%8F%E9%9B%85%E7%BE%8E%E5%A5%B3%E4%B8%8D%E8%BE%9E%E8%BE%9B%E8%8B%A6%E4%B8%BA%E5%A4%A7%E5%AE%B6%E8%B0%8B%E7%A6%8F%E5%88%A9%E6%AF%8F%E5%A4%A9%E4%BF%AE%E6%94%B9BUG%E6%90%9C%E5%88%AE%E6%B5%B7%E6%8A%A5%E4%BB%98%E5%87%BA%E4%BA%86%E5%A4%A7%E9%87%8F%E5%BF%83%E8%A1%80%EF%BC%8C%E8%AF%B7%E5%A4%A7%E5%AE%B6%E5%B0%8A%E9%87%8D%E5%B0%8F%E9%9B%85%E5%8A%B3%E5%8A%A8%E6%9E%9C%E5%AE%9E%EF%BC%8C%E6%89%93%E8%B5%8F%E4%BD%9C%E8%80%85%E4%B8%BA%E7%9F%A5%E8%AF%86%E4%BB%98%E8%B4%B9%E3%80%82%E5%B0%8F%E9%9B%85%E8%BF%98%E5%9C%A8%E4%B8%8D%E6%96%AD%E8%BF%9B%E5%8C%96%E8%AF%B7%E5%A4%A7%E5%AE%B6%E4%BF%9D%E6%8C%81%E5%85%B3%E6%B3%A8%EF%BC%8C%E5%B0%8F%E9%9B%85%E5%AE%98%E7%BD%91%E5%9C%B0%E5%9D%80%EF%BC%9A[alist.xiaoya.pro](alist.xiaoya.pro)%E3%80%82%20%20%E4%BD%9C%E8%80%85%E5%A3%B0%E6%98%8E%E6%9C%AC%E6%96%87%E6%97%A0%E5%88%A9%E7%9B%8A%E7%9B%B8%E5%85%B3%EF%BC%8C%E6%AC%A2%E8%BF%8E%E5%80%BC%E5%8F%8B%E7%90%86%E6%80%A7%E4%BA%A4%E6%B5%81%EF%BC%8C%E5%92%8C%E8%B0%90%E8%AE%A8%E8%AE%BA%EF%BD%9E)
