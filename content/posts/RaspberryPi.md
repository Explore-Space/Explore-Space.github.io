---
title: "RaspberryPi"
date: 2019-10-10T19:43:53+08:00
author: "An"
draft: false
toc: true
tags: 
  - RaspberryPi
---

![Cover](https://images.unsplash.com/photo-1560614196-3f8c2daf6677?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="1359739972">
</meting-js>

## 0x00 摘要

树莓派的简介

***「未完成」***

## 0x01 简介

## 0x02 版本

### 版本代号

| Code<br/>代号 | Model<br/>型号 | Revision<br/>版本 | RAM<br/>内存 | Manufacturer<br/>制造商 |
| ------ | ----------------- | -------- | -------| ------------ |
| 900021 | A+                | 1.1      | 512MB | Sony UK      |
| 900032 | B+                | 1.2      | 512MB | Sony UK      |
| 900092 | Zero              | 1.2      | 512MB | Sony UK      |
| 900093 | Zero              | 1.3      | 512MB | Sony UK      |
| 9000c1 | Zero W            | 1.1      | 512MB | Sony UK      |
| 9020e0 | 3A+               | 1.0      | 512MB | Sony UK      |
| 920092 | Zero              | 1.2      | 512MB | Embest       |
| 920093 | Zero              | 1.3      | 512MB | Embest       |
| 900061 | CM                | 1.1      | 512MB | Sony UK      |
| a01040 | 2B                | 1.0      | 1GB   | Sony UK      |
| a01041 | 2B                | 1.1      | 1GB   | Sony UK      |
| a02082 | 3B                | 1.2      | 1GB   | Sony UK      |
| a020a0 | CM3               | 1.0      | 1GB   | Sony UK      |
| a020d3 | 3B+               | 1.3      | 1GB   | Sony UK      |
| a02042 | 2B (with BCM2837) | 1.2      | 1GB   | Sony UK      |
| a21041 | 2B                | 1.1      | 1GB   | Embest       |
| a22042 | 2B (with BCM2837) | 1.2      | 1GB   | Embest       |
| a22082 | 3B                | 1.2      | 1GB   | Embest       |
| a220a0 | CM3               | 1.0      | 1GB   | Embest       |
| a32082 | 3B                | 1.2      | 1GB   | Sony Japan   |
| a52082 | 3B                | 1.2      | 1GB   | Stadium      |
| a22083 | 3B                | 1.3      | 1GB   | Embest       |
| a02100 | CM3+              | 1.0      | 1GB   | Sony UK      |
| a03111 | 4B                | 1.1      | 1GB   | Sony UK      |
| b03111 | 4B                | 1.1      | 2GB   | Sony UK      |
| c03111 | 4B                | 1.1      | 4GB   | Sony UK      |

### 版本对比

***Via:「[树莓派实验室](http://shumeipai.nxez.com/intro-faq)」***

![001](/Image/posts/RaspberryPi/001.png)

### 细节

#### GPIO

- 40 PIN

![GPIO_40PIN](/Image/posts/RaspberryPi/002.png)

P.S. 靠近 SoC 侧的 GPIO 引脚为奇数编号

- 26 PIN

其引脚对应于上表的前 26 Pin

## 0x 致谢

- [revision-codes](https://github.com/raspberrypi/documentation/tree/master/hardware/raspberrypi/revision-codes) by [Raspberry Pi](https://github.com/raspberrypi)

- [Raspberry Pi 树莓派版本代号大全](http://shumeipai.nxez.com/raspberry-pi-revision-codes) by [树莓派实验室](http://shumeipai.nxez.com/)

- [树莓派介绍以及FAQ](http://shumeipai.nxez.com/intro-faq) by [树莓派实验室](http://shumeipai.nxez.com/)

- [树莓派 40Pin 引脚对照表](http://shumeipai.nxez.com/raspberry-pi-pins-version-40) by [树莓派实验室](http://shumeipai.nxez.com/)
