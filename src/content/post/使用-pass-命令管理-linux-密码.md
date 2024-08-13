---
title: 使用 pass 命令管理 Linux 密码
description: ''
date: 'Mon Jan 15 2024 16:13:08 GMT+0800 (中国标准时间)'
dateFormatted: 'Mon Jan 15 2024 16:13:08 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# 使用 pass 命令管理 Linux 密码

**作者：Thomas Tuffin（Sudoer，Red Hat）**

密码管理是近十年来的热门话题。通过快速的谷歌搜索，你会发现各种选择密码管理工具的选项，以保护解锁个人信息的字符串。一些应用程序仅在计算机上运行，并以加密格式离线存储密码。另一些功能更丰富，提供与多个设备的在线同步、密码共享、双因素身份验证（2FA）等。然而，这些服务中的一些，由于在线库的便利性，使密码管理的简单性在提供的功能海洋中失落，同时也失去了对数据的一些控制，因为您的凭据与您无法控制的服务器同步。

有一种替代方案可以提供简单性并让您完全掌控您的凭据。它可以提供许多与付费服务相同的功能，同时保持其简单性。它是开源的，并由创建 Wireguard 的同一作者编写，该项目在进入 Linux 内核之前受到了 Linus Torvalds 的高度赞扬。这个替代方案被称为 pass，也被称为 password-store。

**为什么使用 password-store?**
- 它是开源的
- 使用简单
- 文档完善
- 基于命令行，但有可用的图形界面扩展
- 使用 GnuPG 加密，加密级别由您选择
- 完全在您的掌控之下。密码不同步到第三方服务器
- 您的密码存储可以仅保留在您的系统上，或者您可以将其与您选择的私有 Git 存储库同步（强烈建议）

**安装**
1. 安装 pass：
   ```
   $ sudo dnf install pass
   ```

2. 如果您还没有 GPG 密钥对，需要创建一个：
   ```
   $ gpg2 --full-generate-key
   ```
   选择选项 1（RSA 和 RSA）作为密钥类型。选择您想要的密钥大小，例如选择 4096。然后选择密钥有效期，在这个示例中选择两年。

3. 现在，列出您的密钥并记下密钥 ID：
   ```
   $ gpg2 --list-secret-keys --keyid-format LONG
   ```

4. 使用您的 GPG 密钥 ID 初始化 pass 数据存储：
   ```
   $ pass init 'AAAA2222CCCC4444'
   ```

5. 现在您可以从 RSA4096 加密的密码存储中生成和获取密码。例如，生成一个新密码：
   ```
   $ pass generate -c Internet/github.com 21
   ```
   获取存储中的密码：
   ```
   $ pass show Internet/github.com
   ```

**附加步骤**
一个 pass 的默认安装为您提供了一个安全的本地数据存储。但为了提高可用性，我认为有几个其他功能是重要的。

**同步到 Git 存储库**

为了实现冗余性和在多个设备之间共享凭据，强烈建议将 pass 存储与 Git 存储库同步。pass 已经内置了 Git 功能，您只需在 pass 存储中创建远程存储库并初始化即可。以下是使用 Github 的示例，但请记住，您可以使用任何版本控制托管提供商或设置自己的托管服务。

1. 在远程 Git 服务器上设置私有存储库后，需要在本地使用以下命令初始化 pass 存储并添加远程 origin：
   ```
   $ pass git init
   ```
   ```
   Initialized empty Git repository in /home/myhome/.password-store/.git/
   [master (root-commit) 998c8fd] Added current contents of password store. 1 file changed, 1 insertion(+)
   create mode 100644 .gpg-id
   ```

   ```
   $ pass git remote add origin git@github.com:johndoe/pass-store.git
   ```

2. 只要您对存储库的身份验证正确配置，就可以使用内置的 pass git push 命令将 pass 存储推送到远程存储库：
   ```
   $ pass git push -u --all
   ```

   ```
   Enumerating objects: 14, done.
   Counting objects: 100% (14/14), done.
   Delta compression using up to 12 threads
   Compressing objects: 100% (12/12), done.
   Writing objects: 100% (12/12), 2.68 KiB | 913.00 KiB/s, done.
   Total 12 (delta 6), reused 0 (delta 0), pack-reused 0
   To git@github.com:johndoe/pass-store.git
     212af8c..d1c11c5  master -> master
   ```

完成后，您的 pass 存储将与远程存储库同步。
