---
title: "Ventoy"
date: 2020-05-17T16:38:13+08:00
author: "An"
draft: false
toc: true
tags: 
  - 
---



---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="19711382">
</meting-js>

## 0x00 摘要

***「未完成」***

## 0x01 简介

*Ventoy* 是一个制作可启动U盘的开源工具。有了Ventoy就无需反复地格式化U盘，只需要把ISO文件拷贝到U盘里面就可以启动。

## 0x02 使用说明

>[Ventoy使用说明](https://www.ventoy.net/cn/index.html)
>
>[Ventoy下载地址](https://www.ventoy.net/cn/download.html)

### 安装

#### Windows

##### 下载

下载安装包，例如 `ventoy-1.0.00-windows.zip` ，然后解压

##### 运行

直接执行 `Ventoy2Disk.exe` 如下图所示，选择U盘设备，然后点击 `安装` 或 `升级` 即可。

![界面](/Image/posts/Ventoy/001.PNG)

##### 说明

>*安装包内 Ventoy 版本*：当前安装包中的Ventoy版本号
>
>*设备内部 Ventoy 版本*：U盘中已安装的Ventoy版本号，如果为空则表示未安装
>
>*安装*：把Ventoy安装到U盘，只有第一次的时候需要，其他情况就只需要Update升级即可
>
>*升级*：升级U盘中的Ventoy版本，升级不会影响ISO文件

#### Linux

##### 下载

下载安装包，例如 `ventoy-1.0.00-linux.tar.gz` ，然后解压

##### 运行

在该文件夹根目录下以 ***root*** 权限执行 `sh Ventoy2Disk.sh -i /dev/XXX` ,其中 `/dev/XXX` 是U盘对应的设备名，比如 `/dev/sdb`

##### 说明

>Ventoy2Disk.sh  选项  /dev/XXX
>
>  选项含义:
>    -i   安装ventoy到磁盘中 (如果对应磁盘已经安装了ventoy则会返回失败)
>    -I   强制安装ventoy到磁盘中 (不管原来有没有安装过)
>    -u   升级磁盘中的ventoy版本

### 拷贝ISO文件

安装完成之后，U盘会被分成两个区。第一个分区将会被格式化为exFAT文件系统，只需要把ISO文件拷贝到这里面即可。你可以把ISO文件放在任意目录以及子目录下。 Ventoy会遍历所有的目录和子目录，找出所有的ISO文件，并按照字母排序之后显示在菜单中。

>**注意**
>
>ISO文件的全路径中(包括目录、子目录和文件名)不能包含中文或者空格

### 升级 Ventoy

如果Ventoy发布了新版本之后，可以点击 `升级` 进行升级，或者Linux系统中使用 `-u` 选项进行升级。

>**注意**
>
>升级操作是安全的，不会影响原有的ISO文件

## 0x03 致谢

- [Ventoy-official](https://www.ventoy.net/)

- [Ventoy-Github](https://github.com/ventoy/Ventoy) by [Ventoy](https://github.com/ventoy)