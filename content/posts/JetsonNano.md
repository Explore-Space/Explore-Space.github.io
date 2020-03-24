---
title: "JetsonNano"
date: 2020-03-24T08:30:23+08:00
author: "An"
draft: false
toc: true
tags: 
  - JetsonNano
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
        id="35625821">
</meting-js>

## 0x00 摘要

JetsonNano

***「待完善」***

## 0x01 简介



## 0x02 简介



## 0x03 首次使用

[入门文档](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit)

### 烧录镜像

下载 [标准镜像](https://developer.nvidia.com/jetson-nano-sd-card-image) 后，将其烧录至 microSD 卡

P.s. 笔者推荐使用[Etcher](https://www.balena.io/etcher) 

### 设置和首次启动

![](/Image/posts/JetsonNano/002.gif)

#### 准备

1. 将microSD卡（已写入系统映像）插入Jetson Nano模块底部的插槽中

![](/Image/posts/JetsonNano/003.png)

2. 连接显示器与鼠标键盘
3. 连接Micro-USB电源（5V⎓2A），Micro-USB连接器旁边的绿色LED会点亮 (Jetson Nano缺省上电自启) 

#### 首次启动

Jetson Nano Developer Kit将进行一些初始设置，包括：

- 查看并接受NVIDIA Jetson软件EULA
- 选择系统语言，键盘布局和时区
- 创建用户名，密码和计算机名
- 登录

#### 登录后

将显示以下画面

![](/Image/posts/JetsonNano/004.png)

### FAQ

#### 功率

如果 Jetson Nano Developer Kit 无法启动或突然断电重启，有可能是电源功率不足，可尝试更换更大功率的电源

***P.S. 关于电源问题后文将详述***

#### 显示

Jetson Nano Developer Kit 支持 HDMI/DP 视频输出，但不支持HDMI到DVI适配器

## 0x04 配置

### 更换软件源

[JetPack](https://developer.nvidia.com/embedded/jetpack) 缺省软件源为国外的源，国内使用不方便故更换为清华源

1. 防止误操作无法恢复，首先备份原本的 `source.list`

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

2.更换为清华源

用以下内容替换 `source.list` 中所有内容

```list
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic main multiverse restricted universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-security main multiverse restricted universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-updates main multiverse restricted universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-backports main multiverse restricted universe
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic main multiverse restricted universe
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-security main multiverse restricted universe
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-updates main multiverse restricted universe
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-backports main multiverse restricted universe
```

## 0x0 致谢

- [Jetson Nano Developer Kit入门](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit) by [NVIDIA](https://developer.nvidia.com/embedded-computing)

- [jetcard](https://github.com/NVIDIA-AI-IOT/jetcard) by [NVIDIA-AI-IOT](https://github.com/NVIDIA-AI-IOT)

- [Jetson Nano更换软件源](https://blog.csdn.net/qq_36396941/article/details/88903094) by [Yeah2333](https://blog.csdn.net/qq_36396941)

- []() by []()

- []() by []()

- []() by []()

- []() by []()

- []() by []()

- []() by []()

- []() by []()

- []() by []()

