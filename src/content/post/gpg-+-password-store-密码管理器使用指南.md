---
title: GPG + Password Store 密码管理器使用指南
description: ''
date: 'Mon Jan 15 2024 01:16:47 GMT+0800 (中国标准时间)'
dateFormatted: 'Mon Jan 15 2024 01:16:47 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# GPG + Password Store 密码管理器使用指南

在本文中，我们将介绍如何安装和配置 GPG 密钥，以及如何使用 Password Store 密码管理器来管理您的密码。我们还会涵盖如何在 iOS、macOS 和 Windows 系统上使用密码

# 为什么开源软件闭源会引起问题？

最近在Hacker News上看到jsiepkes爆料GitHub要求下架EdgeFS开源项目分支的消息，理由是上游项目闭源了。这不是第一次发生这样的事情，国内也曾发生类似事件，但这篇文章不详细叙述历史问题，感兴趣的可以自行搜索。

## 开源社区风气问题

文章指出国内大多数软件从业人员对开源社区的风气了解不够。虽然许多顶级开发者推崇开源，但很少提到或介绍自由软件。作者认为国内开源社区过于浮躁，利益至上，违背了开源运动初衷，更符合实用主义的利益至上价值观。

## 开源许可协议和闭源问题

为什么开源软件闭源后会有问题呢？文章解释了主要的开源许可协议，如GPL/LGPL、BSD、Apache、Mozilla、MIT。许可协议要求在使用、修改、分发代码时遵循一定条件，而某些协议如BSD对商业集成较为友好。

## 自由软件和GPLV3

文章简要介绍了自由软件，强调GPL作为对抗版权的理想主义选择。对于GPLV3有一些人批评其激进性，但作者支持其合作共赢的方式。国内的商业公司也积极参与自由软件和开源软件，改善了过去的不良影响。

## 自由软件不等于免费

作者澄清自由软件并非免费软件，强调在日常生活中自由软件的广泛应用，例如Android系统和访问的互联网网页。文章认为自由软件的出现加速了整个软件和互联网行业的进程。

## 自由软件与开源软件的选择

文章强调选择使用自由软件或开源软件的重要性，认为这些软件具有国际化、成熟、稳定的特点，对小型公司及团队创业有利。在选择软件时，作者建议关注项目作者的道德问题。

## 结语和声明

作者承认文章无法在短时间内全面讲述自由软件和开源软件的知识，鼓励读者自行阅读相关资料。文章以感谢国内自由软件支持者和前辈为结尾，感谢导师的耐心指导。最后，作者声明文章使用emacs-orgmode编写，感谢自由软件与开源软件世界的贡献。

[原文链接](https://news.ycombinator.com/item?id=23113226) | [GNU自由软件哲学](https://www.gnu.org/philosophy/free-sw.zh-cn.html) | [Eric S. Raymond的《大教堂与集市》](https://book.douban.com/subject/25881855/)

# 使用自由软件和开源软件打造网络账号密码管理系统

## 说明

由于涉及到相关自由软件和开源软件工具，前几章节将介绍这些工具的使用。本文面向会电脑操作、对账号密码、隐私有要求的人。如果您熟悉相应工具，建议直接跳过，只阅读不了解的部分。

## 需求

1. 密码存储安全加密唯一性（只能由加密的人才可解密）。
2. 密码随机生成，任意长度、指定包含数字、特殊字符、字符大小写等。
3. 密码易用性、可维护性、可通用性（跨平台设备）。

根据以上需求，采用非对称加密是最合适的选择。

## 非对称加密

非对称加密是密码学的一种算法，需要两个密钥：一个是公开密钥，另一个是私有密钥。公钥用于加密，私钥用于解密。使用公钥加密的数据只能用相应的私钥解密。GPG是非对称加密运用较广泛的实现。

## GPG（GNU Privacy Guard）

GPG是非对称加密的实现，几乎在Linux系统上随处可见。在其他系统上也很容易使用。

### 安装和生成密钥

1. 安装GPG，运行以下命令：

   ```
   gpg --help
   ```

   确认显示GPG的帮助信息，表示安装成功。

2. 生成密钥，运行以下命令：

   ```
   gpg --full-generate-key
   ```

   根据提示选择加密算法、密钥长度、有效期等，最后提供个人信息和设置私钥密码。

### 密钥管理

- 列出已有密钥：

  ```
  gpg --list-keys
  ```

- 删除密钥：

  ```
  gpg --delete-key [用户ID]
  ```

### 导入和导出密钥

- 导出公钥：

  ```
  gpg --armor --output public-key.txt --export [用户ID]
  ```

- 导出私钥：

  ```
  gpg --armor --output private-key.txt --export-secret-keys
  ```

- 导入密钥：

  ```
  gpg --import [公私密钥文件]
  ```

### 加密和解密

- 加密文件：

  ```
  gpg --recipient [用户ID] --output demo.sig --encrypt demo.txt
  ```

- 解密文件：

  ```
  gpg --decrypt demo.sig --output demo.txt
  ```

### 签名

- 签名文件：

  ```
  gpg -u [用户id] --sign demo.txt
  ```

- 验证签名：

  ```
  gpg --verify demo.txt.asc demo.txt
  ```

这些工具可以帮助您建立一个安全、加密、唯一的网络账号密码管理系统。希望本文对您有帮助，如果觉得不错，请帮忙转发关注，感谢支持！未完待续！

```markdown
# 如何使用自由软件和开源软件打造自己的网络账号密码管理

## 说明
由于使用到了相关自由软件和开源软件工具，所以前几章节都是工具使用介绍。文章面向的受众是会电脑操作，对账号密码、隐私有要求的人；相对专业人士来讲，可能比较啰嗦。所以，如果你熟悉对应的工具，建议直接跳过去，看不了解的部分。

## 需求
1. 密码存储安全加密唯一性（只能由加密的人才可解密）。
2. 密码随机生成，任意长度、指定包含数字、特殊字符、字符大小写等。
3. 密码管理易用性、可维护性、可通用性（跨平台设备）。

根据以上需求，密码存储加密唯一性，采用非对称加密最合适。

### 非对称加密
非对称加密是密码学的一种算法，它需要两个密钥，一个是公开密钥，另一个是私有密钥；公钥用作加密，私钥则用作解密。使用公钥把明文加密后所得的密文，只能用相对应的私钥才能解密并得到原本的明文。由于加密和解密需要两个不同的密钥，故被称为非对称加密；不同于加密和解密都使用同一个密钥的对称加密。公钥可以公开，可任意向外发布；私钥不可以公开，必须由用户自行严格秘密保管，绝不透过任何途径向任何人提供。

### GPG
GPG是非对称加密运用比较广泛的实现，几乎在Linux系统上能随处可见。在其他系统上使用也非常简单容易。

1. 安装GPG，可以到官方网站根据所使用的操作系统下载对应的可执行程序。
2. 安装完成后，使用`gpg --help`命令检查是否安装成功。
3. 生成密钥：`gpg --full-generate-key`，根据提示选择密钥种类、长度、有效期等。
4. 列出系统中已有的密钥：`gpg --list-keys`。
5. 导出公钥：`gpg --armor --output public-key.txt --export [用户ID]`。
6. 导出私钥：`gpg --armor --output private-key.txt --export-secret-keys`。
7. 导入密钥：`gpg --import [公私密钥文件]`。

### 密码随机性
在密码学中，对一个序列的随机性是指：“看起来是随机的，即能通过我们所能找到的所有正确的随机性检验。” 这个序列是不可预测的，即使给出产生序列的算法或者硬件设计和以前产生序列的所有知识，也不可能通过计算来预测下一个比特是什么或者计算代价很大几乎不可实现。

随机数生成器有真随机和伪随机之分。这里通过洗牌算法来打乱字符和特殊符号，再通过定长密码位数来随机获取打乱的字符和符号组成新的字符串。

```python
import random

def shuffle_char() -> list:
    """生成乱序的字符串"""
    lst = [...]  # 省略字符列表
    random.shuffle(lst)
    return lst

def shuffle_symbol() -> list:
    """生成乱序的符号"""
    lst = [...]  # 省略符号列表
    random.shuffle(lst)
    return lst

def mod(size: int) -> int:
    r = size % 6
    if size % 6 > 6:
        return mod(r)
    else:
        return r

def generate_password(size: int = 6, include_symbol: bool = True) -> str:
    data = shuffle_char()
    symbols = shuffle_symbol()
    result = []

    symbol_size = 0
    if size < 6:
        return ""
    if include_symbol:
        symbol_size = mod(len(symbols) + len(data))
        if symbol_size == 0:
            symbol_size = 3

    for index in range(0, size - symbol_size):
        i = random.randint(0, len(data) - 1)
        result.append(data[i])
        if symbol_size > 0:
            i = random.randint(0, len(symbols) - 1)
            result.append(symbols[i])
            symbol_size -= 1

    random.shuffle(result)
    return "".join(result)
```

### 使用password-store
password-store是一个PC端使用的自由软件，支持跨平台设备，加密采用GPG加密。以下是安装和基本使用步骤：

1. 安装：
   - Mac上使用brew：`brew install pass`
   - Linux发行版使用包管理器安装，如Fedora: `dnf install pass`，RHEL/CentOS: `yum install pass`，Debian/Ubuntu: `apt-get install pass`，Arch Linux: `pacman -S pass`

2. 初始化密码仓库：
   - `pass init`

3. 生成密码：
   - `pass generate mysite 20`

4. 查看密码树状结构：
   - `pass`

```markdown
## 获取密码

有两种方法可以获取密码：

1. 第一种会显示密码到终端上，方法是运行：

    ```bash
    pass mysite
    ```

2. 更好的方法是使用 `-c` 选项让 `pass` 将密码直接拷贝到剪切板上：

    ```bash
    pass -c mysite
    ```

   两种方法都会要求你输入 GPG 密码。

如果你需要重命名某个站点的名字可以使用：

```bash
pass mv mysite demo
```

同时也可以用相同的密码：

```bash
pass cp demo demo2
```

使用 `rm` 删除账号密码：

```bash
pass rm demo2
```

这几个操作都会对文件进行改变，特别是修改和删除需要谨慎，不过有了接下来的远程仓库，就不担心历史文件被删除了。

### 使用 Git 仓库存储密码

`pass` 可以将密码存放的目录当成 Git 仓库来用，通过版本管理系统能让我们管理密码更方便。

虽然这个功能很方便，但是切记，远程仓库最好设置为私有，避免别人访问，虽然密码文件已经加密，要是万一私钥泄漏，就会全军覆没。Git 的使用请关注下一章节。

```bash
pass git init
```

这会创建 Git 仓库，并自动提交所有已存在的文件。下一步就是指定远程仓库了：

```bash
pass git remote add <name> <url>
```

我们可以把这个密码仓库当成私有代码仓库。唯一的不同点在于每次我们新增或修改一个密码，`pass` 都会自动将该文件加入本地仓库。

更新远程仓库的密码，可以使用 Git 的子命令：

```bash
pass git pull
```

将本地仓库推送至远程仓库：

```bash
pass git push
```

如果你不习惯使用命令行，可以选择其他图形化客户端来使用它，也是可以的，推荐 `qtpass` 这个实现，它是跨平台的。如果是移动端，那么下载对应平台的 APP 即可。

如果你正在使用 1Password 等软件，`pass` 官方还提供迁移工具。

参考 [https://www.passwordstore.org/](https://www.passwordstore.org/)

这章节先到此。未完待续！！
```

需求
密码存储安全加密唯一性（只能由加密的人才可解密）。
密码随机生成，任意长度、指定包含数字、特殊字符、字符大小写等。
密码管理易用性、可维护性、可通用性（跨平台设备）。

根据前面介绍，了解了加密工具、密码生成工具、这章节将介绍安全存储。

数据存储不外乎，采用数据库、文本文件等方式。由于，我们有加密工具可对文件进行加解密，所以，我们将选择一种文本格式存储文件即可，对当前文件进行版本管理，这里就要介绍git的使用了。

Git是什么
Git是目前世界上最先进的分布式版本控制系统。与CVS、Subversion一类的集中式版本控制工具不同，它采用了分布式版本库的做法，不需要服务器端软件，就可以运作版本控制，使得源代码的发布和交流极其方便。git的速度很快，这对于诸如Linux内核这样的大项目来说自然很重要。git最为出色的是它的合并追踪（merge tracing）能力。


初级篇

Git 命令专用名词的译名
-   Workspace：工作区
-   Index / Stage：暂存区
-   Repository：仓库区（或本地仓库）
-   Remote：远程仓库
新建仓库

在自己系统中打开终端（或者使用git图形化工具也可以），这里我们采用命令行，新创建一个文件夹来当作一个仓库，并使用Git初始化这个仓库。
mkdir demo
git init
或者
git init [文件夹名称]

如果是在github、gitlab这种托管服务器上，那么可以使用clone子命令克隆远程仓库到本地。
git clone [url]
配置

Git的设置文件为.gitconfig，它可以放在系统用户主目录下（全局配置），也可以在仓库目录下（只配置当前仓库）。
# 显示当前的Git配置
$ git config --list
# 编辑Git全局配置文件
$ git config -e [--global]
# 直接配置提交时显示的名字和邮件地址
$ git config --global user.name "[name]"
$ git config --global user.email "[email address]"
增加/删除/修改文件
add子命令用于添加文件到暂存区，同时可以指定多个文件。如果想将当前目录下的所有文件提交至暂存区，在该子命令后输入. 即可，-p 可将多处变化分开提交。
rm子命令用于删除已提交的文件，同样可以指定多个文件。mv表示修改该文件，用于修改名称，路径。
# 添加指定文件到暂存区
$ git add [file1] [file2] ...
# 添加指定目录到暂存区，包括子目录
$ git add [dir]
# 添加当前目录的所有文件到暂存区
$ git add .
# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p
# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...
# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]
# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
    
代码提交

提交文件到本地仓库， -m指定提交说明消息来说明这次提交的是什么。同时可以将暂存区指定的文件提交到本地仓库。-a 表示对上一次提交进行追加。-v提交时要求显示所有不同的地方。--amend表示修改上一次提交。
# 提交暂存区到仓库区
$ git commit -m [message]
# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message]
# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a
# 提交时显示所有diff信息
$ git commit -v
# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]
# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
远程同步
fetch子命令获取远程仓库的所有变动，pull 子命令取回远程仓库的变动并合并本地仓库，push上传本地仓库至远程仓库。
# 下载远程仓库的所有变动
$ git fetch [remote]
# 显示所有远程仓库
$ git remote -v
# 显示某个远程仓库的信息
$ git remote show [remote]
# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]
# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]
# 上传本地指定分支到远程仓库
$ git push [remote] [branch]
# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force
# 推送所有分支到远程仓库
$ git push [remote] --all
git clone
远程操作第一步，用于克隆一个远程仓库代码。例如：
# 克隆一份 Emacs 配置
$ git clone git@gitlab.org/7ym0n/dotfairy.git
该命令会在本地主机生成一个目录，与远程主机的版本库同名。如果要指定不同的目录名，可以将目录名作为git clone命令的第二个参数。
$ git clone <版本库的网址> <本地目录名>
git clone支持多种协议，除了HTTP(s)以外，还支持SSH、Git、本地文件协议等，下面是一些例子。
$ git clone http[s]://example.com/path/to/repo.git/
$ git clone ssh://example.com/path/to/repo.git/
$ git clone git://example.com/path/to/repo.git/
$ git clone /opt/git/project.git
$ git clone file:///opt/git/project.git
$ git clone ftp[s]://example.com/path/to/repo.git/
$ git clone rsync://example.com/path/to/repo.git/
git remote
为了便于管理，Git要求每个远程主机都必须指定一个主机名。git remote命令就用于管理主机名。
不带选项的时候，git remote命令列出所有远程主机。
$ git remote 
origin
使用-v选项，可以参看远程主机的网址。
$ git remote -v
origin    git@gitlab.com:7ym0n/dotfairy.git (fetch)
origin    git@gitlab.com:7ym0n/dotfairy.git (push)
上面命令表示，当前只有一台远程主机，叫做origin，以及它的网址。
克隆版本库的时候，所使用的远程主机自动被Git命名为origin。如果想用其他的主机名，需要用git clone命令的-o选项指定。
$ git clone -o my-dotfairy https://gitlab.org/7ym0n/dotfairy.git
$ git remote
my-dotfairy #表示，克隆的时候，指定远程主机叫做my-dotfairy
git remote show命令加上主机名，可以查看该主机的详细信息。
$ git remote show origin
* remote origin
  Fetch URL: git@gitlab.com:7ym0n/dotfairy.git
  Push  URL: git@gitlab.com:7ym0n/dotfairy.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
git remote add命令用于添加远程主机。
$ git remote add <主机名> <仓库地址>
git remote rm命令用于删除远程主机。
$ git remote rm <主机名>
git remote rename命令用于远程主机的改名。
$ git remote rename <原主机名> <新主机名>
git fetch
一旦远程主机的版本库有了更新（Git术语叫做commit），需要将这些更新取回本地，这时就要用到git fetch命令。
$ git fetch <远程主机名>
git fetch命令通常用来查看其他人的进程，因为它取回的代码对你本地的开发代码没有影响。
默认情况下，git fetch取回所有分支（branch）的更新。如果只想取回特定分支的更新，可以指定分支名。
$ git fetch <远程主机名> <分支名>
比如，取回origin主机的master分支。
$ git fetch origin master
所取回的更新，在本地主机上要用"远程主机名/分支名"的形式读取。比如origin主机的master，就要用origin/master读取。
git branch命令的-r选项，可以用来查看远程分支，-a选项查看所有分支。
$ git branch -r
origin/master

$ git branch -a
* master
  remotes/origin/master
取回远程主机的更新以后，可以在它的基础上，使用git checkout命令创建一个新的分支。
$ git checkout -b newBrach origin/master #表示，在origin/master的基础上，创建一个新分支
此外，也可以使用git merge命令或者git rebase命令，在本地分支上合并远程分支。
# 表示在当前分支上，合并origin/master
$ git merge origin/master
# 或者
$ git rebase origin/master
git pull
git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。它的完整格式稍稍有点复杂。
$ git pull <远程主机名> <远程分支名>:<本地分支名>
比如，取回origin主机的develop分支，与本地的master分支合并，需要写成下面这样。
$ git pull origin develop:master
如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
$ git pull origin develop
# 实质上，这等同于先做git fetch，再做git merge
$ git fetch origin
$ git merge origin/develop
在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系（tracking）。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动"追踪"origin/master分支。
Git也允许手动建立追踪关系。
$ git branch --set-upstream master origin/develop
如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。
$ git pull origin
如果当前分支只有一个追踪分支，连远程主机名都可以省略。
$ git pull #当前分支自动与唯一一个追踪分支进行合并。
如果合并需要采用rebase模式，可以使用–rebase选项。
$ git pull --rebase <远程主机名> <远程分支名>:<本地分支名>
如果远程主机删除了某个分支，默认情况下，git pull 不会在拉取远程分支的时候，删除对应的本地分支。这是为了防止，由于其他人操作了远程主机，导致git pull不知不觉删除了本地分支。
但是，你可以改变这个行为，加上参数 -p 就会在本地删除远程已经删除的分支。
$ git pull -p
# 等同于下面的命令
$ git fetch --prune origin
$ git fetch -p
git push
git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相仿。
$ git push <远程主机名> <本地分支名>:<远程分支名>
注意，分支推送顺序的写法是<来源地>:<目的地>，所以git pull是<远程分支>:<本地分支>，而git push是<本地分支>:<远程分支>。
如果省略远程分支名，则表示将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。
$ git push origin master 
# 将本地的master分支推送到origin主机的master分支。
# 如果后者不存在，则会被新建。
# 如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。
$ git push origin :master
# 等同于
$ git push origin --delete master
如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。
$ git push origin
如果当前分支只有一个追踪分支，那么主机名都可以省略。
$ git push
如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。
$ git push -u origin master
上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。
不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。如果要修改这个设置，可以采用git config命令。
$ git config --global push.default matching
# 或者
$ git config --global push.default simple
还有一种情况，就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用–all选项。
$ git push --all origin
如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做git pull合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用–force选项。
$ git push --force origin #使用--force选项，结果导致远程主机上更新的版本被覆盖。除非你很确定要这样做，否则应该尽量避免使用--force选项
最后，git push不会推送标签（tag），除非使用–tags选项。
$ git push origin --tags

注意：如果你是普通用户，比如只是用来管理密码文件什么的，到这里基本够用了，接下来的长篇将是详细介绍命令清单，以及专业用户遇到问题时可能有用的命令介绍。



高级篇


分支
# 列出所有本地分支
$ git branch
# 列出所有远程分支
$ git branch -r
# 列出所有本地分支和远程分支
$ git branch -a
# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]
# 新建一个分支，并切换到该分支
$ git checkout -b [branch]
# 在git 2.23版本过后分支管理使用git switch
# 新建一个分支 并且换到该分支
$ git switch -c [branch]
# 新建一个分支，并切换到该分支，如果该分支存在将强制覆盖旧分支
$ git switch -C [branch]
# 新建一个分支，指向指定commit
$ git branch [branch] [commit]
# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]
# 切换到指定分支，并更新工作区
$ git checkout [branch-name]
# 切换到上一个分支
$ git checkout -
# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream [branch] [remote-branch]
# 合并指定分支到当前分支
$ git merge [branch]
# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]
# 删除分支
$ git branch -d [branch-name]
# 强制删除分支
$ git branch -D [branch-name]
# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
标签
# 列出所有tag
$ git tag
# 新建一个tag在当前commit
$ git tag [tag]
# 新建一个tag在指定commit
$ git tag [tag] [commit]
# 删除本地tag
$ git tag -d [tag]
# 删除远程tag
$ git push origin :refs/tags/[tagName]
# 查看tag信息
$ git show [tag]
# 提交指定tag
$ git push [remote] [tag]
# 提交所有tag
$ git push [remote] --tags
# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
查看信息
# 显示有变更的文件
$ git status
# 显示当前分支的版本历史
$ git log
# 显示commit历史，以及每次commit发生变更的文件
$ git log --stat
# 搜索提交历史，根据关键词
$ git log -S [keyword]
# 显示某个commit之后的所有变动，每个commit占据一行
$ git log [tag] HEAD --pretty=format:%s
# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
$ git log [tag] HEAD --grep feature
# 显示某个文件的版本历史，包括文件改名
$ git log --follow [file]
$ git whatchanged [file]
# 显示指定文件相关的每一次diff
$ git log -p [file]
# 显示过去5次提交
$ git log -5 --pretty --oneline
# 显示所有提交过的用户，按提交次数排序
$ git shortlog -sn
# 显示指定文件是什么人在什么时间修改过
$ git blame [file]
# 显示暂存区和工作区的差异
$ git diff
# 显示暂存区和上一个commit的差异
$ git diff --cached [file]
# 显示工作区与当前分支最新commit之间的差异
$ git diff HEAD
# 显示两次提交之间的差异
$ git diff [first-branch]...[second-branch]
# 显示今天你写了多少行代码
$ git diff --shortstat "@{0 day ago}"
# 显示某次提交的元数据和内容变化
$ git show [commit]
# 显示某次提交发生变化的文件
$ git show --name-only [commit]
# 显示某次提交时，某个文件的内容
$ git show [commit]:[filename]
# 显示当前分支的最近几次提交
$ git reflog
撤销
# 恢复暂存区的指定文件到工作区
$ git checkout [file]
# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]
# 恢复暂存区的所有文件到工作区
$ git checkout .
# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]
# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard
# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]
# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]
# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]
# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]
# 暂时将未提交的变化移除，稍后再移入
$ git stash
$ git stash pop
其他
# 生成一个可供发布的压缩包
$ git archive
仓库管理


git bisect
git bisect是一个很有用的命令，用来查找哪一次代码提交引入了错误。它的原理很简单，就是将代码提交的历史，按照两分法不断缩小定位。所谓"两分法"，就是将代码历史一分为二，确定问题出在前半部分，还是后半部分，不断执行这个过程，直到范围缩小到某一次代码提交。git bisect start命令启动查错，它的格式如下。
$ git bisect start [终点] [起点]
例如：选择全部的代码历史。起点是第一次提交186356c，终点是最近一次的HEAD。当然，指定其他范围也可以。
$ git bisect start HEAD 186356c
确定正常工作。使用git bisect good命令，标识本次提交（第N次）没有问题。
$ git bisect good
确定不能正常工作。使用git bisect bad命令，标识本次提交（第N次）有问题。
$ git bisect bad
接下来，不断重复这个过程，直到成功找到出问题的那一次提交为止。这时，Git 会给出如下的提示。
is the first bad commit
然后，使用git bisect reset命令，退出查错，回到最近一次的代码提交。
$ git bisect reset
git cherry-pick
对于多分支的代码库，将代码从一个分支转移到另一个分支是常见需求。这时分两种情况。一种情况是，你需要另一个分支的所有代码变动，那么就采用合并（git merge）。另一种情况是，你只需要部分代码变动（某几个提交），这时可以采用 Cherry pick。git cherry-pick命令的作用，就是将指定的提交（commit）应用于其他分支。
$ git cherry-pick <commitHash> 
# 将指定的提交commitHash，应用于当前分支。这会在当前分支产生一个新的提交，
# 当然它们的哈希值会不一样。
git cherry-pick命令的参数，不一定是提交的哈希值，分支名也是可以的，表示转移该分支的最新提交。
$ git cherry-pick feature
Cherry pick 支持一次转移多个提交。
$ git cherry-pick <HashA> <HashB> # 将 A 和 B 两个提交应用到当前分支。这会在当前分支生成两个对应的新提交。
# 如果想要转移一系列的连续提交，可以使用下面的简便语法。
$ git cherry-pick A..B # 它们必须按照正确的顺序放置：提交 A 必须早于提交 B，否则命令将失败，但不会报错。
注意，使用上面的命令，提交 A 将不会包含在 Cherry pick 中。如果要包含提交 A，可以使用下面的语法。
$ git cherry-pick A^..B
git cherry-pick命令的常用配置项如下。
（1）-e，–edit
打开外部编辑器，编辑提交信息。
（2）-n，–no-commit
只更新工作区和暂存区，不产生新的提交。
（3）-x
在提交信息的末尾追加一行(cherry picked from commit …)，方便以后查到这个提交是如何产生的。
（4）-s，–signoff
在提交信息的末尾追加一行操作者的签名，表示是谁进行了这个操作。
（5）-m parent-number，–mainline parent-number
如果原始提交是一个合并节点，来自于两个分支的合并，那么 Cherry pick 默认将失败，因为它不知道应该采用哪个分支的代码变动。
-m配置项告诉 Git，应该采用哪个分支的变动。它的参数parent-number是一个从1开始的整数，代表原始提交的父分支编号。
$ git cherry-pick -m 1 <commitHash> 
# Cherry pick 采用提交commitHash来自编号1的父分支的变动。
# 一般来说，1号父分支是接受变动的分支（the branch being merged into），
# 2号父分支是作为变动来源的分支（the branch being merged from）。
如果操作过程中发生代码冲突，Cherry pick 会停下来，让用户决定如何继续操作。
（1）–continue
用户解决代码冲突后，第一步将修改的文件重新加入暂存区（git add .），第二步使用下面的命令，让 Cherry pick 过程继续执行。
$ git cherry-pick --continue
（2）–abort
发生代码冲突后，放弃合并，回到操作前的样子。
（3）–quit
发生代码冲突后，退出 Cherry pick，但是不回到操作前的样子。
Cherry pick 也支持转移另一个代码库的提交，方法是先将该库加为远程仓库。
$ git remote add target git://gitUrl
$ git fetch target # 将远程代码仓库抓取到本地。
$ git log target/master # 检查一下要从远程仓库转移的提交，获取它的哈希值。
$ git cherry-pick <commitHash> # 使用git cherry-pick命令转移提交。
撤销操作
一种常见的场景是，提交代码以后，你突然意识到这个提交有问题，应该撤销掉，这时执行下面的命令就可以了。
$ git revert HEAD
命令的原理是，在当前提交后面，新增一次提交，抵消掉上一次提交导致的所有变化。它不会改变过去的历史，所以是首选方式，没有任何丢失代码的风险。git revert 命令只能抵消上一个提交，如果想抵消多个提交，必须在命令行依次指定这些提交。比如，抵消前两个提交，要像下面这样写。
$ git revert [倒数第一个提交] [倒数第二个提交]
git revert命令还有两个参数。–no-edit：执行时不打开默认编辑器，直接使用 Git 自动生成的提交信息。–no-commit：只抵消暂存区和工作区的文件变化，不产生新的提交。


丢弃提交
如果希望以前的提交在历史中彻底消失，而不是被抵消掉，可以使用git reset命令，丢弃掉某个提交之后的所有提交。
$ git reset [last SHA]
git reset的原理是，让最新提交的指针回到以前某个时点，该时点之后的提交都从历史中消失。
默认情况下，git reset不改变工作区的文件（但会改变暂存区），–hard参数可以让工作区里面的文件也回到以前的状态。
$ git reset --hard [last good SHA]
执行git reset命令之后，如果想找回那些丢弃掉的提交，可以使用git reflog命令。不过，这种做法有时效性，时间长了可能找不回来。


替换上一次提交
提交以后，发现提交信息写错了，这时可以使用git commit命令的–amend参数，可以修改上一次的提交信息。
$ git commit --amend -m "Fixes bug #42"
它的原理是产生一个新的提交对象，替换掉上一次提交产生的提交对象。
这时如果暂存区有发生变化的文件，会一起提交到仓库。所以，–amend不仅可以修改提交信息，还可以整个把上一次提交替换掉。


撤销工作区的文件修改
如果工作区的某个文件被改乱了，但还没有提交，可以用git checkout命令找回本次修改之前的文件。
$ git checkout -- [filename]
它的原理是先找暂存区，如果该文件有暂存的版本，则恢复该版本，否则恢复上一次提交的版本。
注意，工作区的文件变化一旦被撤销，就无法找回了。

从暂存区撤销文件
如果不小心把一个文件添加到暂存区，可以用下面的命令撤销。
$ git rm --cached [filename] # 不影响已经提交的内容。
# 最新版本的git推荐使用restore，撤销部分变更
$ git restore --staged [file]
# 撤销所有变更
$ git restore --staged .
# 撤销所有变更
$ git reset -- .
# 撤销暂存区部分变更
$ git reset -- [file1] [file2]
代码回滚
你在当前分支上做了几次提交，突然发现引入大量bug，导致代码稳定性，可以执行以下操作。
# 代码回滚，不影响历史
$ git revert [commit-id]

# 撤销丢弃，影响历史提交记录
$ git reset --hard [当前分支此前的最后一次提交] # 远程分支的该操作一定要团队达成共识，否则很容易导致版本混乱冲突，代码丢失
江湖救急
在某些场景下，执行提交代码后，忘记提交至远程仓库后，执行了git reset指令，导致代码当前分支下的所有工作被重置。可以使用以下命令拯救愚蠢的操作。
# 查看历史操作记录,该记录存在本地，如果本地仓库被彻底破坏，神仙也救不了了。
$ git reflog
# 使用git reset --hard 恢复
$ git reset --hard [command-id]
# 也可以使用git cherry-pick恢复
$ git cherry-pick [command-id]
丢弃工作区所有不受版本控制的文件和目录
$ git clean -fdx
核弹级操作
例如，在某些人不经思考把一些二进制文件或包含认证密码信息的文件提交至仓库，可以使用以下命令进行清理。
# 删除所有分支中的特殊文件
$ git filter-branch --tree-filter 'rm -f [file]' HEAD
# --tree-filter 该参数会在每次检出时先执行命令然后重新提交结果
