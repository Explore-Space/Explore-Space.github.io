---
title: "Ubuntu"
date: 2018-12-07T23:55:03+08:00
author: "An"
draft: false
toc: true
tags:
  - Linux 
  - Ubuntu
  - 折腾日志
---

![Cover](https://images.unsplash.com/photo-1559274604-bf3a06409885?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="32019002">
</meting-js>

## 0x00 摘要

Ubuntu 的安装与配置

## 0x01 前言

虽然在虚拟机和备用机上多次安装过许多Linux发行版，但在物理机上安装 Ubuntu ，还是免不了遇到各种各样的问题，所以写下这篇文章记录过程。

## 0x02 内容

- 基本情况
  - 软件
    - OS:
      - Ubuntu 18.04(LTS)
      - Ubuntu 18.10
  - 硬件
    - 型号: 联想拯救者R720
      - CPU: i5-7300HQ
      - 内存： 8G DDR4
      - 显卡： GTX 1050Ti(4G)
      - SSD:
        - 1: 128G NVME (Samsung)
        - 2: 512G NVME (Hikvision-C2000Pro)
      - HDD: 1T (Western Digital)
      - 无线网卡: QCA9377
      - 其余接口:
        - 1Gbps LAN口
        - 3.5mm 耳机接口
        - HDMI * 1
        - USB2.0(Type-A) * 1
        - USB3.0 Gen1(Type-A) * 2
        - USB3.0 Gen1(Type-C) * 1(是否为全功能Type-C未测试)

### 引导

常见的引导方式有两种 *BIOS + MBR* ， *UEFI + GPT*，后者相较于前者有着诸多优点，也是未来的趋势，故笔者选用后者

### 硬盘

在 BIOS 硬盘相关设置中

```text
SATA Controller Mode

[AHCI]
Set SATA controller to AHCI mode.
[Intel RST Premium]
Set SATA controller to Interl RST Premium(RAID) mode.
```

默认选择后者，这会导致安装过程中，无法识别到固态硬盘，只有选到 AHCI 模式才可以。

>**存疑**
>
>后来查阅资料后发现后者好像是需要驱动才可用，似乎对固态性能影响不大，故没有再关注这个问题

### 显卡

#### 现象

安装完成后，重启过程中报错

```bash
kernel:NMI watchdog: BUG: soft lockup - CPU#0 stuck for 26s
```

强制关机后重启进入桌面，有明显卡顿感，几秒后系统进入假死状态

#### 原因

>**存疑**
>
>CPU 过度使用， Linux 的内核锁死或者死循环导不能进入系统。最新的内核已经把视频模式设置嵌入内核中，所以所有显卡硬件程序的指定时钟和寄存器当图形服务器启动时在内核进行而不是图形设备运行，这使得在启动时可以看到不闪的和高分辨率的好看的启动界面，但是，在某些视频卡它不能正常工作而现实黑屏。

#### 解决

##### 启用核显

在 BIOS 启动后，进入系统前，按 *Esc*  进入 grub 选择界面，按 *E* 编辑 grub ，在 `quiet splash` 后插入 `nomodeset` ，按 *F10* 或 *Ctrl* + *X* 保存后即可正常启动

启动后修改 grub 配置文件，默认禁用独显(后文会详述独显驱动安装，该处为方便暂时只用核显)。修改 `/etc/default/grub` 同上

更新 grub 配置

```bash
sudo update-grub
```

##### 启用独显

安装NVIDIA驱动(Ubuntu 18.04/18.10中可在 软件和更新 → 附加驱动 中找到开源和闭源驱动)

还原 grub 配置文件，即删除 `/etc/default/grub` 中 `quiet splash` 后的 `nomodeset`

更新 grub 配置

```bash
sudo update-grub
```

如图,安装成功
![效果](/Image/posts/Ubuntu/001.png)

##### 插曲

>Linux creator Linus Torvalds talked in front of students at the Aalto University Center for Entrepreneurship in Otaniemi, Finland. The chat and its Q&A session was around an hour long and while the bulk of it is probably quite interesting, the best bit — by far — occurs at the 49-minute mark when Torvalds delivers his very frank opinion of NVIDIA and its support for Linux.
>
>Linux的创造者Linus Torvalds在芬兰奥塔涅米的阿尔托大学创业中心的学生面前讲话。聊天和问答环节大约有一个小时，虽然大部分内容可能都很有趣，但迄今为止最好的一点发生在49分钟的时候，当时torvalds发表了他对nvidia及其对linux支持的非常坦率的意见。
>
>One of the students asks for Torvalds' thoughts on NVIDIA and its reportedly poor support for its Optimus technology in Linux. The purpose of Optimus is to allow notebooks to dynamically switch between an Intel integrated graphics chip and an NVIDIA one, as performance requirements demand.
>
>其中一名学生询问了torvalds对nvidia的看法，以及据说nvidia在linux中对optimus技术的支持不足。optimus的目的是允许笔记本电脑根据性能要求在英特尔集成图形芯片和nvidia芯片之间动态切换。
>
>Here's his reply:
>
>他的回答是：
>
>>I know exactly what you're talking about and I'm happy to say that it's the exception rather than the rule. I'm also happy to very publicly point out that NVIDIA has been one of the worst trouble spots we've had with hardware manufacturers.
>>
>>我很清楚你在说什么，我很高兴地说这是个例外，而不是规则。我也很高兴非常公开地指出，nvidia一直是我们与硬件制造商之间最糟糕的问题之一。
>>
>>And that is really sad because NVIDIA tries to sell chips — a lot of chips — into the Android market and NVIDIA has been the single worst company we've every dealt with. So, NVIDIA, fuck you!
>>
>>这真的很可悲，因为英伟达试图把芯片——很多芯片——卖给安卓市场，而且英伟达是我们所有交易中最糟糕的公司。所以，英伟达，**！

### LAN

#### 现象

Ubuntu 18.04 / 18.10 中，无法直接通过 设置 新建PPPOE连接

#### 原因

Ubuntu 18.04 / 18.10 中，采用 GNOME3 作为默认桌面环境，该问题为 GNOME3 的固有问题

#### 解决

##### 方案1(推荐)

其实在 Gnome3 的 NetworkManager 中包含 PPPOE 连接方式，不过无法直接通过桌面环境操作，执行以下命令

```bash
nm-connection-editor
```

在弹出的管理窗口中即可新建PPPOE连接

##### 方案2

使用 pppoeconf 建立 PPPOE 连接

```bash
sudo pppoeconf
```

P.S. 该方法在使用过程不稳定，故不推荐该方法

### WLAN

#### 现象

安装完成后，无线连接不可用，如图

![效果](/Image/posts/Ubuntu/002.png)

#### 原因

执行以下命令

```bash
~$ rfkill list all
```

输出以下内容

```bash
0:ideapad_wlan: Wireless LAN
Soft blocked: no
Hard blocked:yes
1:ideapad_bluetooth: Bluetooth
Soft blocked: no
Hard blocked: yes
2:phy0: Wireless LAN
Soft blocked: no
Hard blocked:no
3:hci0: Bluetooth
Soft blocked: yes
Hard blocked: no
```

可以看到，优先级前的 ideapad_wlan 的 Hard blocked 默认为 yes ，即 Ubuntu 默认关闭了硬件 WLAN 开关，而 R720 这样机型的并没有硬件 WLAN 开关，所以导致 WLAN 无法开启。

#### 解决

##### 暂时

执行以下命令

```bash
sudo modprobe -r ideapad_laptop
```

##### 永久

在 `/etc/modprobe.d/ideapad.conf` 中添加 `blacklist ideapad_laptop` ， 重启

## 0x03 尾巴

今天西安初雪，听说初雪许的愿望想的祝福都会实现,嗯~

![雪景 (Photo by 谭浩声)](/Image/posts/Ubuntu/003.jpeg)
