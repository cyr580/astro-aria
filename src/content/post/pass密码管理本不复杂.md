---
title: pass密码管理本不复杂
description: ''
date: 'Mon Jan 15 2024 05:25:07 GMT+0800 (中国标准时间)'
dateFormatted: 'Mon Jan 15 2024 05:25:07 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# Password Store 使用指南

## 目录

- [Password Store 简介](#password-store-简介)
- [安装](#安装)
  - [GPG 安装与配置](#gpg-安装与配置)
  - [Password Store 安装](#password-store-安装)
- [GPG 密钥生成](#gpg-密钥生成)
- [GPG 密钥导出](#gpg-密钥导出)
- [使用](#使用)
- [同步](#同步)
- [插件](#插件)
- [结语](#结语)

## Password Store 简介

Password Store 是一个简单而强大的密码管理器，它使用 GPG 加密和 Git 同步来存储和管理密码。它具有以下特点：

- 使用标准的 Unix 工具，无复杂依赖
- 使用简单的文件系统层次结构，方便浏览和搜索
- 使用 GPG 加密，保证密码安全性
- 使用 Git 同步，保证密码一致性和可恢复性
- 支持多个平台，包括 Linux、macOS、Windows、Android、iOS 等
- 支持多种插件，扩展功能和用户体验

## 安装

### GPG 安装与配置

在使用 Password Store 之前，您需要先安装并配置 GPG。以下是常见平台上的安装方法：

#### Linux

使用包管理器安装 GPG：

```shell
apt install gnupg  # Ubuntu/Debian
pacman -S gnupg    # Arch Linux
```

#### macOS

使用 Homebrew 安装 GPG：

```shell
brew install gnupg
```

#### Windows

在 Windows 上，您可以使用 Gpg4win 工具包进行安装和配置。请访问 [Gpg4win 官方网站](https://gpg4win.org/) 获取详细指南。

### Password Store 安装

可以通过多种方式安装 Password Store。以下是常见平台上的安装方法：

#### Linux

使用包管理器安装 pass：

```shell
apt install pass  # Ubuntu/Debian
pacman -S pass    # Arch Linux
```

#### macOS

使用 Homebrew 安装 pass：

```shell
brew install pass
```

#### Windows

使用 Chocolatey 安装 pass：

```shell
choco install pass
```

#### Android

从 Google Play 商店安装 Password Store 应用。

#### iOS

从 App Store 安装 Pass for iOS 应用。

更多安装方法和详细文档，请访问 [官方网站](https://www.passwordstore.org/#download)。

## GPG 密钥生成

在使用 Password Store 之前，您需要生成一个 GPG 密钥对。密钥对由公钥和私钥组成，公钥用于加密密码并分享给他人，私钥用于解密密码和签名。

运行以下命令生成 GPG 密钥对：

```shell
gpg --full-generate-key
```

按照提示选择密钥类型、密钥长度、密钥过期时间、真实姓名和电子邮件地址等选项。生成密钥后，您可以使用以下命令查看您的公钥和私钥：

```shell
gpg --list-keys
gpg --list-secret-keys
```

## GPG 密钥导出

如果您希望在其他设备上使用相同的 GPG 密钥对，您需要将密钥导出并导入到目标设备上。

导出公钥，运行以下命令：

```shell
gpg --export -a "Your Name" > public.key
```

将公钥保存到名为 `public.key` 的文件中。

导出私钥，运行以下命令：

```shell
gpg --export-secret-keys -a "Your Name" > private.key
```

将私钥保存到名为 `private.key` 的文件中。

在目标设备上，导入公钥和私钥，运行以下命令：

```shell
gpg --import public.key
gpg --import private.key
```

导入后，您可以使用 `gpg --list-keys` 和 `gpg --list-secret-keys` 命令确认导入是否成功。

请注意，密钥是非常敏感的信息，请妥善保管您的私钥，并且建议将其加密备份到安全的位置。

## 使用

要开始使用 Password Store，您需要先初始化密码存储库。运行以下命令：

```shell
pass init "Your GPG Key ID"
```

这将创建一个名为 `.password-store` 的目录，用于存储密码文件。每个文件都是 GPG 加密的文本，包含密码和可选的元数据（如用户名、网址等）。

使用 pass 命令管理密码文件，例如：

- `pass ls`：列出所有密码文件
- `pass insert foo/bar`：插入名为 foo/bar 的密码文件
- `pass show foo/bar`：显示 foo/bar 的密码文件内容
- `pass edit foo/bar`：编辑 foo/bar 的密码文件内容
- `pass generate foo/bar 16`：生成一个 16 位随机密码，并保存到 foo/bar 的密码文件
- `pass rm foo/bar`：删除 foo/bar 的密码文件
- `pass mv foo/bar foo/baz`：将 foo/bar 重命名为 foo/baz
- `pass cp foo/bar foo/qux`：将 foo/bar 复制为 foo/qux
- `pass grep foo`：搜索包含 foo 的密码文件

更多命令和选项，请使用 `pass --help` 查看或访问 [官方网站](https://www.passwordstore.org/#usage)。

## 同步

Password Store 使用 Git 来同步密码存储库。您可以使用 `pass git` 命令执行任何 Git 命令，例如：

- `pass git init`：初始化 Git 仓库
- `pass git remote add origin https://example.com/repo.git`：添加远程仓库
- `pass git push -u origin master`：将密码存储库推送到远程仓库
- `pass git pull`：从远程仓库拉取更新到密码存储库
- `pass git status`：查看密码存储库的状态
- `pass git log`：查看密码存储库的历史记录

更多 Git 命令和用法，请使用 `pass git --help` 查看或访问 [Git 官方网站](https://git-scm.com/doc)。

## 插件

Password Store 支持多种插件，扩展功能和用户体验。以下是一些常用插件的示例：

- [pass-otp](https://github.com/tadfisher/pass-otp)：支持一次性密码（OTP）的生成和验证
- [pass-tomb](https://github.com/roddhjav/pass-tomb)：支持使用 Tomb 创建隐藏的密码存储库
- [pass-audit](https://github.com/j6k4m8/pass-audit)：支持对密码存储库进行安全性和复杂性的检查
- [pass-update](https://github.com/roddhjav/pass-update)：支持批量更新密码存储库中的密码
- [pass-import](https://github.com/roddhjav/pass-import)：支持从其他密码管理器导入密码到密码存储库

更多插件和列表，请访问[官方网站](https://www.passwordstore.org/#extensions)。

## 结语

Password Store 是一个简单而强大的密码管理器，它使用 GPG 加密和 Git 同步来存储和管理密码。它的优点是简单、安全、一致、多平台和可扩展。如果您正在寻找一个方便且安全的密码管理器，不妨尝试使用 Password Store。😊

了解更多信息，请访问[官方网站](https://www.passwordstore.org/)。

参考资料：
- [Password Store 官方网站](https://www.passwordstore.org/)
- [GPG 官方网站](https://gnupg.org/)
