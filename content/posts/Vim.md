---
title: "Vim"
date: 2019-09-16T23:32:36+08:00
author: "An"
draft: false
toc: true
tags: 
  - Vim
---

![Cover](https://images.unsplash.com/photo-1559808578-e1ba9255a025?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="18284330">
</meting-js>

## 0x00 摘要

Vim 的 “ABC”

***「待完善」***

## 0x01 起源

![001](/Image/posts/Vim/001.jpg)

话要从上面这张图说起，这张图源自Bilibili Up主 [之乎者也-zhzy](https://space.bilibili.com/64648363)。笔者虽然知道 Vim 的强大，但从刚刚接触 Linux 到现在作为主力系统，始终使用 nano 作终端下的编辑器。因为对于笔者来说，终端下的编辑器仅用于更改配置文件，“又不是不能用”(笑)。其实从根本上来说是懒得学习，毕竟 nano 的学习成本低，但简单往往意味着见简陋。于是，笔者决定详细的了解 Vim 。(题外话：以前找资料，Baidu为首选，现在Bilibili为首选)

## 0x02 学习

笔者发现 Bilibili Up主 [TheCW](https://space.bilibili.com/13081489)的 Vim 系列视频很不错，推荐读者去看看。同时该 Up 主的其他视频也推荐读者去看看，讲解的很透彻。

- [TheCW](https://space.bilibili.com/13081489)
  - [Vim_1-av55498503](https://www.bilibili.com/video/av55498503)
  - [Vim_2-av55664166](https://www.bilibili.com/video/av55664166)
  - [Vim_3-av56020134](https://www.bilibili.com/video/av56020134)

## 0x03 安装

以 Manjaro 为例

- 安装 Vim

  ```bash
  sudo pacman -Sy vim
  ```

- 安装 vim-plug

  >[vim-plug](https://github.com/junegunn/vim-plug)
  >
  >A minimalist Vim plugin manager.

  ```bash
  curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
      https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  ```

- 配置

  - 编辑 ` ~/.vimrc ` ，保存退出，以下为例子

    ```text
    " Specify a directory for plugins
    " - For Neovim: stdpath('data') . '/plugged'
    " - Avoid using standard Vim directory names like 'plugin'
    call plug#begin('~/.vim/plugged')

    " Make sure you use single quotes

    " Shorthand notation; fetches https://github.com/junegunn/vim-easy-align
    Plug 'junegunn/vim-easy-align'

    " Any valid git URL is allowed
    Plug 'https://github.com/junegunn/vim-github-dashboard.git'

    " Multiple Plug commands can be written in a single line using | separators
    Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

    " On-demand loading
    Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
    Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

    " Using a non-master branch
    Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

    " Using a tagged release; wildcard allowed (requires git 1.9.2 or above)
    Plug 'fatih/vim-go', { 'tag': '*' }

    " Plugin options
    Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }

    " Plugin outside ~/.vim/plugged with post-update hook
    Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }

    " Unmanaged plugin (manually installed and updated)
    Plug '~/my-prototype-plugin'

    " Initialize plugin system
    call plug#end()
    ```

  - 安装插件

    ```bash
    vim ~/.vimrc
    ```
  
    ```bash
    :PlugInstall
    ```

    等待完成

## 0x04 配置

以下为笔者目前的 Vim 配置

```text
syntax on                 "语法高亮
set number                "显示行号
set norelativenumber      "关闭显示相对行号
set cursorline            "突出显示当前行
set wrap                  "自动折行，即拆分过长的行
set linebreak             "不会在单词内部折行
set showcmd               "命令模式下，在底部显示，当前键入的指令
set wildmenu              "命令模式下，底部操作指令按下 Tab 键自动补全。第一次按下 Tab ，显示所有匹配的操作指令的清单；第二次按下 Tab，会依次选择各个指令
set autoread              "文件监视
set showmatch             "光标遇到括号时，自动高亮对应的另一个括号


set hlsearch              "搜索时，高亮显示匹配结果
exec "nohlsearch"
set incsearch             "
set ignorecase            "搜索时，忽略大小写
set smartcase             "如果同时打开了ignorecase，那么对于只有一个大写字母的搜索词，将大小写敏感；其他情况都是大小写不敏感

"Vim 插件管理器
"Minimalist Vim Plugin Manager
"https://github.com/junegunn/vim-plug

call plug#begin('~/.vim/plugged')

"lean & mean status/tabline for vim that's light as air
Plug 'vim-airline/vim-airline'

"A tree explorer plugin for vim.
Plug 'scrooloose/nerdtree'

call plug#end()

```

## 0x04 致谢

- [TheCW](https://space.bilibili.com/13081489)

- [Vim 配置入门](http://www.ruanyifeng.com/blog/2018/09/vimrc.html) by [阮一峰](http://www.ruanyifeng.com/home.html)
