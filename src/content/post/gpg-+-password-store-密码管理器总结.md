---
title: GPG + Password Store 密码管理器总结
description: ''
date: 'Mon Jan 15 2024 05:25:07 GMT+0800 (中国标准时间)'
dateFormatted: 'Mon Jan 15 2024 05:25:07 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
```markdown
# 如何使用自由软件和开源软件打造自己的网络账号密码管理

## 04

### 说明

由于使用到了相关自由软件和开源软件工具，所以前几章节都是工具使用介绍。文章面向的受众是会电脑操作，对账号密码、隐私有要求的人；相对专业人士来讲，可能比较啰嗦。所以，如果你熟悉对应的工具，建议直接跳过去，看不了解的部分。

### 需求

1. 密码存储安全加密唯一性（只能由加密的人才可解密）。
2. 密码随机生成，任意长度、指定包含数字、特殊字符、字符大小写等。
3. 密码管理易用性、可维护性、可通用性（跨平台设备）。

### 根据前面介绍

了解了加密工具、密码生成工具、安全存储工具；本章将结合前面的工具做一个总结。

## 使用演示

经过前三篇文章 GPG 加密、密码生成与管理、Git 使用基本上已经完成了密码管理的工作了，本章将串联前三篇文章介绍的工具进行各个平台设备的使用演示。

1. 使用 GPG 程序生成公私钥。gpg 名字叫做hacktribe，后面使用的时候 gpg-id 都指定它即可。

    ```bash
    $ gpg --full-generate-key
    ```

2. 确定 pass 命令已经安装好。使用上一步生成公私钥时的名字初始化密码目录，使用默认的目录即可。

    ```bash
    $ pass init hacktribe
    ```

3. 配置好远程私有仓库。用于存放加密后的密码文件。选择创建一个私有的 Git 仓库，如 GitLab，并配置仓库的远程地址。

    ```bash
    $ pass git remote add main git@gitlab.com:hacktribe/password-store.git
    $ pass git pull main
    $ pass git push main
    ```

## 图形化工具使用

一般用户，不会使用命令行？没关系，还可以使用图形管理工具 qtpass 来管理。安装完成后，首次打开，会让配置相关配置。

如果需要自动提交到远程仓库，需要在 settings 中把 Use git，相关的 git push 和 git pull 都选上。

这样就完成了密码备份。

## 结束了吗？

NO!!! 虽然现在完成了基本的使用，但是，现在还有移动设备等其他平台，或者换一台机器后怎么办？

备份 GPG 密钥，采用 U 盘或者打印纸张藏起来。需要使用 `--export-ownertrust` 导出信任的数据。

```bash
gpg --export-ownertrust > file.txt
```

如果导出备份，没有使用该参数，会导致迁移其他平台时，状态是未知不可信的，生成密码等会提示是否知晓自己当前的操作的确认，在某些客户端下可能会导致使用有问题。

It is NOT certain that the key belongs to the person named in the user ID. If you *really* know what you are doing, you may answer the next question with yes.

Use this key anyway? (y/N)

如果不希望提示，可以手动修改为信任：

```bash
$ gpg --edit-key user@useremail.com
gpg> trust
Please decide how far you trust this user...
Your decision? 5
gpg> save
```

## 编辑器集成

小编经常需要用文本编辑器开发程序、写文章什么的，所以，PC端的客户端，只需要安装 password-store 程序，然后通过文本编辑器来管理密码或者一些敏感信息的。

## 移动端使用

这里以 iPhone 为例，到应用商店搜索 "password store" 找到 "pass - password store" 下载即可，或者到 [GitHub](https://mssun.github.io/passforios/) 上下载。

接下来只需要配置好远程仓库即可。可以使用 SSH-key 或者用户名密码进行管理（账号密码就是 GitLab 的登录账号）。

![Configuration](insert_image_url_here)

配置完成，就可以使用了。

![App Screenshots](insert_image_url_here)

密码管理系列文章，到这里就结束了。

### 总结

使用下来，绝对不比商业软件差，就是配置稍微比较麻烦而已。好处在于，可以根据自己的需求改变，例如，你可以把 GitLab 部署在家庭网络里，这样所有数据都由自己保管。不依托第三方服务，不用担心一次性泄漏干干净净，底裤被人扒了。
