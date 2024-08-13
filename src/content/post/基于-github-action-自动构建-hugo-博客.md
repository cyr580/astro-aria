---
title: 基于 Github Action 自动构建 Hugo 博客
description: 描述
date: 'Sat Aug 06 2022 05:54:07 GMT+0800 (中国标准时间)'
dateFormatted: 'Sat Aug 06 2022 05:54:07 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

## 本文主要记录了如何配置 Github Action 实现 Hugo 博客自动部署。
![](https://i.loli.net/2021/03/29/Kwh3819MRgteGn6.jpg)

<!— more —>
### 1. 概述
Hugo 都是静态博客，即最终生成的是静态页面，而所谓部署就是把这些静态文件放到 web 服务器(比如 Nginx、Caddy) 的对应目录就行了。

因此整个 Github Action 只需要做两件事：

* 编译，生成静态文件
* 部署，把静态文件移动到合适的位置
* 比如放到某个云服务器上
* 或者放到 Github Pages
然后我们再通过 git push 来触发 Github Action 就可以了。

### 2. 具体实现

添加 Github Action

需要在仓库根目录下创建 .github/workflow 这个二级目录，然后在 workflow 下以 yml 形式配置 Github Action。

具体可以参考 这个仓库

需要指定 action 触发条件，这里就设置为 push 触发，具体如下：
```on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:
```
以上表示在 main分支收到 push 事件时执行该 action。

如果是之前创建的仓库，可能需要改成 master 分支。

另外我们可以直接在 [marketplace](https://github.com/marketplace?type=actions) 找别人配置好的 action 来使用，就更加方便了，以下是本教程用到的 action

* [actions/checkout](https://github.com/marketplace/actions/checkout)
* [hugo-setup](https://github.com/marketplace/actions/hugo-setup)
* [github-pages-action](https://github.com/marketplace/actions/github-pages-action)
* [rsync](https://github.com/marketplace/actions/rsync-deployments-action)
我们要做的就是把这些单独的 action 进行组合，以实现自动部署。

发布到 Github Pages

静态博客可以直接用 Github Pages，比较简单，缺点就是国内访问会比较慢，甚至于直接打不开。

action 文件如下
```name: GitHub Pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: ‘0.100.2’
          # 是否启用 hugo extend
          extended: true

      - name: Build
        run: hugo —minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: ${{ github.ref == ‘refs/heads/main’ }}
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```
整个 Action 一个包含 4 个步骤：

1. 拉取代码
2. 准备 hugo 环境
3. 使用 hugo 编译生成静态文件
4. 把生成的静态文件发布到 Github Pages
其他都不需要改，唯一需要注意的是 Hugo 的版本以及是否启用 hugo 扩展。

建议改成和自己当前使用的版本，否则可能会出现兼容性问题。
```      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: ‘0.100.2’
          extended: true
```

### 3. 测试

随便修改点内容，执行提交
```echo hello > tmp.txt
git add . 
git commit -m “test action”
```
然后打开 github action 页面查看，可以看到已经在执行了



点开可以查看执行日志



到此，整个配置就完成了，具体细节可以参考 这个仓库

原文作者：意琦行
原文链接：https://www.lixueduan.com/post/blog/01-github-action-deploy-hugo/
