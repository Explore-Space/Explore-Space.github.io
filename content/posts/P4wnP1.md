---
title: "P4wnP1"
date: 2019-10-11T23:45:44+08:00
author: "An"
draft: false
toc: true
tags: 
  - RaspberryPi
  - 渗透测试
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
        id="1396151812">
</meting-js>

## 0x00 摘要

关于 P4wnP1

***「未完成」***

## 0x01 简介

### 基本情况

>P4wnP1 is a highly customizable USB attack platform, based on a low cost Raspberry Pi Zero or Raspberry Pi Zero W.
>
>P4wnP1 是一个基于低成本的树莓派 Zero 或 Zero W的高度可定制的 USB 攻击平台。

### 起源

笔者了解该项目源自于 Bilibili Up主 [取火的普罗米修斯〔无序熵增〕](https://space.bilibili.com/39602674)的视频

- [P4wnP1搭建电脑后门](https://www.bilibili.com/video/av19905867)
- [P4wnP1获取电脑本地账户密码](https://www.bilibili.com/video/av19906566)
- [[硬件黑客]如何制作一个属于自己的骇客硬件](https://www.bilibili.com/video/av20574726)
- [[硬件黑客]bad USB窃取电脑浏览器密码](https://www.bilibili.com/video/av21963736)
- [[硬件黑客]粘滞键后门的安装使用](https://www.bilibili.com/video/av22801556)

题外话，笔者接触 Linux 便是从这里开始的，后来逐渐从树莓派，到虚拟机，再到物理机，从 Raspbian 到 Ubuntu ，再到 Manjaro

## 0x02 硬件

### 主体

#### Raspberry Pi Zero W

##### 硬件参数

- Broadcom BCM2835 1GHz ARM11内核
- 512MB 内存
- 802.11 b/g/n WiFi无线网卡
- 低功耗蓝牙4.1 (BLE)
- Micro SD 卡插槽
- Mini-HDMI接口 (可输出1080p60视频)
- Micro-USB供电接口
- Micro-USB OTG通信接口
- 40PIN GPIO接口焊盘 (兼容A+/B+/2代B/3代B)
- CSI摄像头接口
- 复合视频接口焊盘
- 复位接口接口焊盘
- 尺寸：65mm x 30mm x 5mm

##### 图片

![Zero_W-01](/Image/posts/P4wnP1/Zero_W-01.jpg)

![Zero_W-02](/Image/posts/P4wnP1/Zero_W-02.jpg)

![Zero_W-03](/Image/posts/P4wnP1/Zero_W-03.jpg)

#### Raspberry Pi Zero

##### 硬件参数

- Broadcom BCM2835 1GHz ARM11内核
- 512MB 内存
- Micro SD 卡插槽
- Mini-HDMI接口 (可输出1080p60视频)
- Micro-USB供电接口
- Micro-USB OTG通信接口
- 40PIN GPIO接口焊盘 (兼容A+/B+/2代B/3代B)
- CSI摄像头接口
- 复合视频接口焊盘
- 复位接口接口焊盘
- 尺寸：65mm x 30mm x 5mm

##### 图片

![Zero-01](/Image/posts/P4wnP1/Zero-01.jpg)

![Zero-02](/Image/posts/P4wnP1/Zero-02.jpg)

![Zero-03](/Image/posts/P4wnP1/Zero-03.jpg)

### 附件

P.S. 附件均为可选项

#### USB

P.S. 在 Zero (W) PCB 背面引出了 USB(OTG) 四线焊盘 (Vcc,Gnd,Data+,Data-)，如下图

![PCB_USB](/Image/posts/P4wnP1/PCB_USB.jpg)

##### 类型A

###### 介绍

###### 图片

![USB_1-01](/Image/posts/P4wnP1/USB_1-01.jpg)

![USB_1-02](/Image/posts/P4wnP1/USB_1-02.jpg)

![USB_1-03](/Image/posts/P4wnP1/USB_1-03.jpg)

![USB_1-04](/Image/posts/P4wnP1/USB_1-04.jpg)

![USB_1-05](/Image/posts/P4wnP1/USB_1-05.jpg)

###### 购买

- [盛成威科技](https://m.tb.cn/h.eoKahP7?sm=bc7c78)  *「淘宝」*
- [NXEZ 创客商店](https://m.tb.cn/h.eLRt1j7?sm=1d8a0c)  *「淘宝」*

##### 类型B

###### 介绍

###### 图片

![USB_2-01](/Image/posts/P4wnP1/USB_2-01.jpg)

![USB_2-02](/Image/posts/P4wnP1/USB_2-02.jpg)

![USB_2-03](/Image/posts/P4wnP1/USB_2-03.jpg)

###### 购买

- [WaveShare 微雪电子](https://c.tb.cn/h.eoeagjA?sm=7fe760)  *「淘宝」*
- [NXEZ 创客商店](https://c.tb.cn/h.eo3A2UY?sm=10f8f3)  *「淘宝」*

#### UPS

##### 类型A

###### 介绍

###### 图片

![UPS_1-01](/Image/posts/P4wnP1/UPS_1-01.jpg)

![UPS_1-02](/Image/posts/P4wnP1/UPS_1-02.jpg)

![UPS_1-03](/Image/posts/P4wnP1/UPS_1-03.jpg)

![UPS_1-04](/Image/posts/P4wnP1/UPS_1-04.jpg)

![UPS_1-05](/Image/posts/P4wnP1/UPS_1-05.jpg)

###### 购买

- [XiaoJ工作室](https://c.tb.cn/h.eLRrmC3?sm=8d3d85)  *「淘宝」*

##### 类型B

###### 介绍

P.S. 该 UPS [外壳文件](https://github.com/PiSugar/PiSugar)已在 Github 开源

###### 图片

![UPS_2-01](/Image/posts/P4wnP1/UPS_2-01.jpg)

![UPS_2-02](/Image/posts/P4wnP1/UPS_2-02.jpg)

![UPS_2-03](/Image/posts/P4wnP1/UPS_2-03.jpg)

![UPS_2-04](/Image/posts/P4wnP1/UPS_2-04.jpg)

![UPS_2-05](/posts/P4wnP1/UPS_2-05.png)

###### 购买

- [jdaie](https://market.m.taobao.com/app/idleFish-F2e/widle-taobao-rax/page-detail?wh_weex=true&wx_navbar_transparent=true&id=575556807426)  *「咸鱼」*

## 0x03 软件

### P4wnP1 A.L.O.A.

#### 简介

>P4wnP1 A.L.O.A. by MaMe82 is a framework which turns a Rapsberry Pi Zero W into a flexible, low-cost platform for pentesting, red teaming and physical engagements ... or into "A Little Offensive Appliance".
>
>MaMe82 的 P4wnP1 A.L.O.A 是一个将 Raspberry Pi Zero W 转换成灵活，低成本的用于渗透测试，红方测试，真实攻击的平台，或者变成“一个小小的攻击性工具”
>
>***笔者注:***
>
>1.`pentesting` 为 `penetration test 〔渗透测试〕` 的简写
>
>2.关于 **red teaming**
>>摘自:[ProCheckUp](https://www.procheckup.com/services/security-audit/red-teaming/)
>>
>>For the most authentic penetration test simulation, a technique known as Red Teaming, where the **testers simulate what an attacker in the real world would do** , would be the ideal solution. Often in security testing, penetration testers are restricted by what is allowed to be in scope and the test becomes more of an audit than a reflection of what an attacker would attempt. As a result, clients often do not receive an overall picture of the security posture of their organisation. Red Teaming takes a more realistic approach to attacking the organisation and exploiting any weaknesses.
>>
>>对于最真实的渗透测试模拟来说，一种被称为“红队”的技术，即**测试人员模拟真实世界中的攻击者会做什么**，将是理想的解决方案。通常在安全测试中，渗透测试人员受到允许在范围内的内容的限制，测试更像是一个审计，而不是反映攻击者的企图。因此，客户往往得不到组织安全态势的总体情况。红队采取了一种更现实的方式来攻击组织和利用任何弱点。

#### 安装

- 下载镜像

  [下载链接](https://github.com/mame82/P4wnP1_aloa/releases/download/v0.1.0-alpha2/kali-linux-v0.1.0-alpha2-rpi0w-nexmon-p4wnp1-aloa.img.xz)  {Release date:2018.12.07 Size:873MB}

- 烧录镜像

  解压 `kali-linux-v0.1.0-alpha2-rpi0w-nexmon-p4wnp1-aloa.img.xz` ,将 `kali-linux-v0.1.0-alpha2-rpi0w-nexmon-p4wnp1-aloa.img` 烧录至 Micro SD 卡 ，插入树莓派

- 连接

  >PSK : `MaMe82-P4wnP1`
  >URL : `http://172.24.0.1:8000`
  >Admin : `root`
  >Password : `toor`

#### 效果

***(由于笔者目前手边没有 Windows 电脑，故不方便展示相关功能，后期可能会完善)***

### P4wnP1

#### 简介

>P4wnP1 is a highly customizable USB attack platform, based on a low cost Raspberry Pi Zero or Raspberry Pi Zero W (required for HID backdoor).
>
>P4wnP1 是一个基于一个低成本的 Raspberry Pi Zero or Raspberry Pi Zero W 的高度可定制的 USB 攻击平台
>
>***笔者注:***
>
>1. `HID` 是 `Human Interface Device 〔人机交互设备`的缩写

#### 安装

- 下载镜像

  [下载链接](https://github.com/mame82/P4wnP1/releases/download/v0.1.0-alpha1/P4wnP1_0_1_alpha.zip)  
  
  {Release date:2018.04.08 Size:1020MB}

- 烧录镜像

  解压 `P4wnP1_0_1_alpha.zip` ,将 `  ` 烧录至 Micro SD 卡 ，插入树莓派

#### 效果

***(由于笔者目前手边没有 Windows 电脑，故不方便展示相关功能，后期可能会完善)***

## 0x03 说明

- 本文中出现的所有商品均非广告，笔者仅为读者方便了解硬件信息故附以购买链接

## 0x04 声明

***本文内容仅作学习交流使用，读者若使用该设备，所造成一切后果自负，与本文作者无关。***

## 0x05 致谢

- [P4wnP1_aloa](https://github.com/mame82/P4wnP1_aloa) by [mame82](https://github.com/mame82)

- [P4wnP1](https://github.com/mame82/P4wnP1) by [mame82](https://github.com/mame82)

- [取火的普罗米修斯〔无序熵增〕](https://space.bilibili.com/39602674)
