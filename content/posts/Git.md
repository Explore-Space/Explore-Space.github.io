---
title: "Git"
date: 2019-07-08T12:12:24+08:00
author: "An"
draft: false
toc: true
tags: 
  - Git
---

![Cover](https://images.unsplash.com/photo-1559276452-25949cf1c29d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="451703096">
</meting-js>

## 0x00 摘要

Git 的 “ABC”

## 0x01 简介

>Git is the open source distributed version control system.  <br/>  Git是开源的分布式版本控制系统

## 0x02 Git Cheat Sheet

### A Configure Tooling  〔配置工具〕

- Configure user information for all local repositories  <br/>  为所有本地存储库配置用户信息

>Sets the name you want attached to your commit transactions  <br/>  设置要附加到提交事务的名字

```bash
git config --global user.name "[name]"
```

>Sets the email you want attached to your commit transactions  <br/>  设置要附加到提交事务的邮箱

```bash
git config --global user.email "[email address]"
```

>Enables helpful colorization of command line output  <br/>  启用命令行输出的辅助着色

```bash
git config --global color.ui auto
```

### B Create Repository  〔创建存储库〕

- Start a new repository or obtain one from an existing URL  <br/>  启动新的存储库或从现有URL获得一个存储库

>Creates a new local repository with the specified name  <br/>  使用指定的名称创建新的本地存储库

```bash
git init [project-name]
```

>Downloads a project and its entire version history  <br/>  下载项目及其完整版本历史记录

```bash
git clone [url]
```

### C Make Changes  〔进行更改〕

- Review edits and craft a commit transaction  <br/>  审查编辑并制定提交事务

>Lists all new or modified files to be committed  <br/>  列出所有要提交的新文件或修改过的文件

```bash
git status
```

>Shows file differences not yet staged  <br/>  显示尚未暂存的文件差异

```bash
git diff
```

>Snapshots the file in preparation for versioning  <br/> 快照文件以备版本控制 

```bash
git add [file]
```

>Shows file differences between staging and the last file version  <br/>  显示暂存和上一个文件版本之间的文件差异

```bash
git diff --staged
```

>Unstages the file, but preserve its contents  <br/>  取消暂存文件，但保留其内容

```bash
git reset [file]
```

>Records file snapshots permanently in version history  <br/>  在版本历史记录中永久记录文件快照

```bash
git commit -m "[descriptive message]"
```

### D Group Changes  〔组变更〕

>Lists all local branches in the current repository  <br/>  列出当前存储库中的所有本地分支

```bash
git branch
```

>Creates a new branch  <br/>  创建新分支

```bash
git branch [branch-name]
```

>Switches to the specified branch and updates the working directory  <br/>  切换到指定的分支并更新工作目录

```bash
git checkout [branch-name]
```

>Combines the specified branch’s history into the current branch  <br/>  将指定分支的历史记录合并到当前分支

```bash
git merge [branch]
```

>Deletes the specified branch  <br/>  删除指定的分支

```bash
git branch -d [branch-name]
```

### E Relocate Filenames  〔重定位文件名〕

- Relocate and remove versioned files  <br/>  重新定位并删除版本控制的文件

>Deletes the file from the working directory and stages the deletion  <br/>  从工作目录中删除文件并将删除过程分阶段进行

```bash
git rm [file]
```

>Removes the file from version control but preserves the file locally  <br/>  从版本控制中删除文件，但在本地保留文件

```bash
git rm --cached [file]
```

>Changes the file name and prepares it for commit  <br/>  更改文件名并准备提交

```bash
git mv [file-original] [file-renamed]
```

### F Suppress Tracking  〔抑制追踪〕

- Exclude temporary files and paths  <br/>  排除临时文件和路径

>A text file named .gitignore suppresses accidental versioning of files and paths matching the specified patterns  <br/>  名为.gitignore的文本文件可禁止意外地对与指定模式匹配的文件和路径进行版本控制

```bash
*.log
build/
temp-*
```

>Lists all ignored files in this project  <br/>  列出该项目中所有忽略的文件

```bash
git ls-files --other --ignored --exclude-standard
```

### G Save Fragments  〔保存片段〕

>Temporarily stores all modified tracked files  <br/>  临时存储所有已修改的跟踪文件

```bash
git stash
```

>Restores the most recently stashed files  <br/>  还原最近保存的文件

```bash
git stash pop
```

>Lists all stashed changesets  <br/>  列出所有保存的变更集 

```bash
git stash list
```

>Discards the most recently stashed changeset  <br/>  丢弃最近保存的变更集

```bash
git stash drop
```

### H Review History  〔回顾历史〕

- Browse and inspect the evolution of project files  <br/>  浏览并检查项目文件的演变

>Lists version history for the current branch  <br/>  列出当前分支的版本历史记录

```bash
git log
```

>Lists version history for a file, including renames  <br/>  列出文件的版本历史，包括重命名

```bash
git log --follow [file]
```

>Shows content differences between two branches  <br/>  显示两个分支之间的内容差异

```bash
git diff [first-branch]...[second-branch]
```

>Outputs metadata and content changes of the specified commit  <br/>  输出指定提交的元数据和内容更改

```bash
git show [commit]
```

### I Redo Commits  〔重提交〕

- Erase mistakes and craft replacement history  <br/>  清除错误和*制作* **「存疑」** 更换历史

>Undoes all commits after [commit] , preserving changes locally  <br/>  撤消[commit]之后的所有提交，在本地保留更改

```bash
git reset [commit]
```

>Discards all history and changes back to the specified commit  <br/>  放弃所有历史记录并更改回指定的提交

```bash
git reset --hard [commit]
```

### J Synchronize Changes  〔同步变更〕

- Register a repository bookmark and exchange version history  <br/>  注册存储库书签并交换版本历史记录

>Downloads all history from the repository bookmark  <br/>  从存储库书签下载所有历史记录

```bash
git fetch [bookmark]
```

>Combines bookmark’s branch into current local branch  <br/>  将书签分支合并到当前本地分支

```bash
git merge [bookmark]/[branch]
```

>Uploads all local branch commits to GitHub  <br/>  上传所有本地分支提交到GitHub

```bash
git push [alias] [branch]
```

>Downloads bookmark history and incorporates changes  <br/>  下载书签历史记录并合并更改

```bash
git pull
```

## 0x03 常用命令

### 配置

- 配置名字

  ```bash
  git config --global user.name "□□□□□"
  ```

  P.S. □□□□□ 为你的名字

- 配置邮箱

  ```bash
  git config --global user.email "□□□□□"
  ```

  P.S. □□□□□ 为你的邮箱

- 配置 SSH

  - 生成 SSH Key

    ```bash
    ssh-keygen -t rsa -C "□□□□□"
    ```

    P.S. □□□□□ 为你的邮箱

  - 查看并复制公钥

    ```bash
    cat □□□□□
    ```

    P.S. □□□□□ 为公钥路径，默认路径为 `~/.ssh/id_rsa.pub`

  - 添加SSH公钥

    在 Github 中 `Personal settings` - `SSH and GPG keys` 添加公钥即可

### 使用

- 提交至暂存区

  ```bash
  git add all
  ```

- 提交至 HEAD

  ```bash
  git commit -m "□□□□□"
  ```

  P.S. □□□□□ 为代码提交信息

- 提交至远端仓库

  ```bash
  git push
  ```

## 0x04 致谢

- [Git for All Platforms](https://git-scm.com)

- [Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)

- [Git 大全](https://gitee.com/all-about-git) by [码云](https://gitee.com/)
