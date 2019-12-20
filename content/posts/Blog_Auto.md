---
title: "Hugo 自动部署"
date: 2019-12-17T23:31:18+08:00
author: "An"
draft: false
toc: true
tags: 
  - Blog
  - Github Actions
---

![Cover](https://images.unsplash.com/photo-1560953470-9e400a5bb7c3?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="27759600">
</meting-js>

## 0x00 摘要

基于 Hugo 的 Blog 搭建与自动部署配置

## 0x01 起源

起初，笔者觉得 [Hexo](https://hexo.io/) 无疑是最好的博客框架，友好的配置与丰富的主题及插件。但极慢的加载速度消耗着笔者的耐心，最终下定决心再一次重构 Blog。这次笔者采用对加载速度优化更好的 [Hugo](https://gohugo.io/) 框架。笔者之前采用 [Travis-ci](https://travis-ci.org) 实现自动部署，目前其网站处于被墙的边缘，而且属于第三方服务，目前 [Github Actions](https://github.com/features/actions) 已发布正式版，故笔者决定采用 Actions 实现自动部署。

最终，新 Blog 的方案确定: ~~[Hexo](https://hexo.io/)~~ ***[Hugo](https://gohugo.io/)*** + ~~[Travis-ci](https://travis-ci.org)~~ ***[Github Actions](https://github.com/features/actions)***

## 0x02 搭建

笔者本地环境为:

- OS: *Manjaro 18.1.4 Juhraya*
- Kernel: *Linux 5.4.2-1-MANJARO*
- Hugo: *v0.60.1/extended linux/amd64*

>**预期效果**
>
>1.在特定仓库下有两个分支:
>
>>① source: 默认分支，存储整个 Blog 的源代码
>>
>>② master: 主分支，存储生成的静态页面，并以此生成 Github Page
>
>2.利用 Github Actions 实现自动部署，即: 向 source 分支推送文章或配置更改，由 Actions 编译生成静态页面，推送至 master 分支，更新 Github Page 实现对 Blog 的更改

P.S. 方案不止这一种，但笔者觉得这样最方便，最符合笔者需求，故下文均以此方案为基础

### 创建仓库

在 Github 上创建仓库，仓库名为 ***`□□□□□.github.io`*** 。创建时为方便下部操作建议勾选 *Initialize this repository with a README* 。

P.S. □□□□□ 为你的 Github 用户名

### 创建分支

仓库创建完成后，点击左侧 *Branch: master* ，输入  ***`source`***

P.S. ***`source`*** 可自行更改，下文 source 分支均指存储 Blog 所有源代码的分支

### 更改默认分支

仓库创建后默认分支为 master 分支，为方便管理，需更改 source 为默认分支。将仓库的 *Settings* → *Branches* → *Default branch* 修改为 ***`source`*** 分支

### 添加SSH部署密钥

在本地终端执行以下命令生成部署密钥。执行完成后，会在当前目录下生成 `gh-pages.pub` 「公钥」 和 `gh-pages` 「私钥」

```bash
ssh-keygen -t rsa -b 4096 -C "$(git config user.email)" -f gh-pages -N ""
```

P.S. 上述命令中 `$(git config user.email)` 可直接替换为邮箱地址

进入仓库的 *Settings* 中:

- 在 *Deploy keys* 中添加公钥; **Title** 自定义即可，**Key** 则填入 `gh-pages.pub` 「公钥」 的内容，并勾选 `Allow write access`

  - 添加公钥

  ![添加公钥](/Image/posts/Blog_Auto/deploy-keys-1.jpg)

  - 成功

  ![成功](/Image/posts/Blog_Auto/deploy-keys-2.jpg)

- 在 *Secrets* 中添加私钥; **Name** 填入 `ACTIONS_DEPLOY_KEY`，**Value** 则填入`gh-pages` 「私钥」

  - 添加私钥

  ![添加私钥](/Image/posts/Blog_Auto/secrets-1.jpg)

  - 成功

  ![成功](/Image/posts/Blog_Auto/secrets-2.jpg)

>**注意！！！**
>
>在添加私钥时需格外注意，`gh-pages` 「私钥」 的格式大致如下
>
>```text
>-----BEGIN OPENSSH PRIVATE KEY-----
>□□□...□□
>□□□...□□
>...
>□□□...□□
>-----END OPENSSH PRIVATE KEY-----
>```
>
>在 *Secrets* 中 **Value** 需填入`gh-pages` 所有内容。即包括 `-----BEGIN OPENSSH PRIVATE KEY-----` 和 `-----END OPENSSH PRIVATE KEY-----` 以及之间的密钥
>
>笔者在部署时，并没有意识到这一点，在这里卡了很久。笔者只在 **Value** 中填入其中的密钥部分。在之后的 Github Actions 部署过程中总是报错，大致意思是 没有仓库的写入权限 。

### 创建 Hugo 站点

执行以下命令，会在当前目录下生成 Hugo 站点的标准文件

```bash
hugo new site Blog
```

P.S. 上述命令中 `Blog` 可自行定义

使用 `git clone` 命令将远端的 ***`□□□□□.github.io`*** 仓库 clone 到本地，然后将生成的 Blog 文件夹下所有内容复制至本地 ***`□□□□□.github.io`*** 仓库，并进入该仓库文件夹

### 添加主题

>主题来源:[Hugo Themes](https://themes.gohugo.io/)
>
>以下以笔者使用的主题 [hermit](https://github.com/Track3/hermit) 为例

P.S. 多数 Hugo 主题仓库下都会有相应说明文件

在 Hugo 站点的根目录(即本地 ***`□□□□□.github.io`*** 仓库)下执行以下命令添加主题

```bash
git clone https://github.com/Track3/hermit.git themes/hermit
```

操作可选:

- 执行以下命令将此主题存储库作为 git 子模块包含在内。适用于不需要对主题进行深度定制，或希望轻松的获取主题更新 **「推荐」** 后续操作均以此为基础

```bash
git submodule add https://github.com/Track3/hermit.git themes/hermit
```

- 删除主题存储库下的 `.git` 文件夹，将主题文件直接作为 ***`□□□□□.github.io`*** 仓库的组成

### 添加配置 Github Actions 配置文件

参考: [actions-gh-pages](https://github.com/peaceiris/actions-gh-pages/blob/master/README.md)

>简单说明一下 Github Actions 的工作原理(以 Blog 自动部署为例)，不一定准确但简单易懂：
>
>常规情况下，部署 Hugo 站点需要手动在本地编译出静态文件，然后将其推送至远端，生成静态网页。而 Actions 相当于远端有一台 Linux 虚拟机，当检测到你的仓库 source 分支有变化时，会将你的仓库克隆下来，编译后将生成的静态文件推送至远端仓库 master 分支。
>
>因为远端的虚拟机需要拉取及推送仓库，所以需要有仓库的读写权限，这样就很容易理解上文 *[添加SSH部署密钥](/posts/blog_auto/#ssh)* 中的操作

在 Hugo 站点的根目录(即本地 ***`□□□□□.github.io`*** 仓库)下，新建 `.github/workflows/gh-pages.yml` 文件

以下为笔者的配置文件

```YAML
name: github pages

on:
  push:
    branches:
    - source

jobs:
  build-deploy:
    runs-on: ubuntu-18.04
    steps:
    - uses: actions/checkout@v1
      # with:
      #   submodules: true

    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: '0.59.1'
        # extended: true

    - name: Build
      run: |
        git clone https://github.com/Track3/hermit.git themes/hermit
        hugo --minify

    - name: Deploy
      uses: peaceiris/actions-gh-pages@v2
      env:
        ACTIONS_DEPLOY_KEY: ${{ secrets.ACTIONS_DEPLOY_KEY }}
        PUBLISH_BRANCH: master
        PUBLISH_DIR: ./public
```

- P.S.
  
  - 分支相关

    配置文件头部以下部分中，`source` 为站点源代码存储分支，需根据实际情况修改

    ```YAML
    on:
      push:
        branches:
        - source
    ```

  - hugo-version 相关

    Hugo 目前最新版为 **0.60.1**，但笔者目前[2019-12-17 23:31:18]在测试中遇到了Bug: Markdown 文件中 HTML 部分无法渲染，故笔者采用 **0.59.1** 部署 Blog

  - Hugo 主题相关

    上文 *[添加主题](/posts/blog_auto/#heading3)* 中，笔者将主题仓库作为笔者仓库的子模块。这样当执行 `git clone` 时，不会将子模块一同 clone 下来，即站点 `/themes` 是空的

    ↓ `/themes` 为空时，站点 HTML 文件渲染错误，报错信息如下

    ![报错](/Image/posts/Blog_Auto/Error_001.png)

    解决：在执行 `hugo --minify` 之前添加以下内容，手动将主题文件 clone 下来

    ```bash
    git clone https://github.com/Track3/hermit.git themes/hermit
    ```

### 推送

完成上述步骤后，将本地仓库推送至远端，等待 Action 完成自动部署，完成后稍等即可访问 `□□□□□.github.io` 查看站点内容。

P.S. □□□□□ 为你的 Github 用户名

- 关于时间

  - 推送完成到 Github Actions 开始动作: 约 1 s

  - Github Actions 开始动作到部署完成: 约 40 s

  - 初次部署完成到站点正常访问: 约 3 min

  - 更新部署完成到站点更新: 约 5 s

## 0x03 问题

>笔者觉得相比于结果解决问题的过程和思路更重要，故记录笔者遇到问题及解决的思路

### 密钥添加

笔者在上文 *[添加SSH部署密钥](/posts/blog_auto/#ssh)* 的 *注意* 中，也提到了因为私钥添加错误导致卡了很久。笔者看到 Actions 报错，本能的以为是其配置文件有问题(Actions 正式发布没多久，所以相应的文档较少)，所以反复尝试: 修改 Github Actions 配置文件，推送至远端，等待...一如既往的报错。笔者也很沮丧，甚至想放弃 ***[Hugo](https://gohugo.io/) + [Github Actions](https://github.com/features/actions)*** 重新采用 ***[Hexo](https://hexo.io/) + [Travis-ci](https://travis-ci.org)*** 。

等笔者静下心，查看 Actions 的报错信息时，发现前面环境部署以及静态文件的编译都完成了，就最后推送至远端仓库时，写入权限报错。笔者开始逆向查找问题，首先检查的便是 *公钥* 与 *私钥* ，很快就发现了问题所在，修复后问题解决。

### Git 子模块

在 Actions 完成部署后，笔者访问站点一看傻眼了

![报错](/Image/posts/Blog_Auto/Error_001.png)

笔者首先利用 `hugo server` 检查了本地仓库是否正常，本地可以正常生成站点;然后又检查了远端仓库 master 分支，Actions 正确的将静态文件文件推送进来，笔者想不通哪里出了问题。

笔者根据网页显示的报错信息四处检索，忽然看到有人说是不是站点下没有 HTML 文件。笔者重新检查了 master 分支，的确在根目录下只有 `index.xml` ，而没有 `index.html` 。但笔者还是想不明白问什么会这样，继续检索。最后，笔者在 Hugo Github 仓库的 Issues 下看到，有人因为生成 Hugo 标准文件后直接部署而没有添加主题，遇到了与我同样的报错。笔者马上反应过来，在本地尝试 clone 仓库，发现 `/themes` 文件夹下为空，终于找到问题的根源了。解决也很简单，修改 Actions 的配置文件，在部署前添加 clone 主题仓库的命令即可。重新推送后，查看master 分支，增加了 `index.html` ，站点访问正常。

## 0x04 致谢

- [HUGO](https://gohugo.io/)

- [Hermit](https://github.com/Track3/hermit) by [Track3](https://github.com/Track3/)

- [Github Actions](https://github.com/features/actions)

- [actions-hugo](https://github.com/peaceiris/actions-hugo) by [peaceiris](https://github.com/peaceiris)

- [actions-gh-pages](https://github.com/peaceiris/actions-gh-pages) by [peaceiris](https://github.com/peaceiris)
