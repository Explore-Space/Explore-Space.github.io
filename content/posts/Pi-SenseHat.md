---
title: "Pi:SenseHat"
date: 2019-10-18T23:15:44+08:00
author: "An"
draft: false
toc: true
tags: 
  - RaspberryPi
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
        id="1338149101">
</meting-js>

## 0x00 摘要

关于树莓派附件：SenseHat

## 0x01 简介

>The Sense HAT is an add-on board for Raspberry Pi, made especially for the Astro Pi mission.
>
>Sense HAT 是专门为 Astro Pi 任务而制造的 Raspberry Pi 附加板，

P.S. 欧洲 [Astro Pi](https://astro-pi.org/) 挑战赛通过编写在国际空间站上的 Raspberry Pi 计算机上运行的计算机程序，为年轻人提供了进行太空科学研究的绝佳机会。Astro Pi是与Raspberry Pi基金会合作开展的ESA教育项目。

- 总览

![001](/Image/posts/Pi-SenseHat/001.jpg)

- 正面

![002](/Image/posts/Pi-SenseHat/002.jpg)

- 反面

![003](/Image/posts/Pi-SenseHat/003.jpg)

- 上电测试图

![004](/Image/posts/Pi-SenseHat/004.jpg)

## 0x02 硬件

- 8×8 RGB LED矩阵

- 5个按键的迷你操纵杆

- 传感器：

  - 陀螺仪

  - 加速度计

  - 磁力计

  - 温度

  - 气压

  - 湿度

## 0x03 Python 库

***「[SenseHat Python](https://pythonhosted.org/sense-hat/)」***

### 安装

```bash
sudo apt-get update
sudo apt-get install sense-hat
sudo reboot
```

### API

#### Hello world

```python
from sense_hat import SenseHat

sense = SenseHat()
sense.show_message("Hello world!")
```

## 0x04 FAQ

### 1

#### Q.

插上去运行示例程序显示
OSError Cannot detect RPi-Sense FB device

#### A.

在针脚接触良好和树莓派I2C开启的前提下，报错oserror cannot detect rpi-sense fb device，可以在 /boot/config.txt 最后加上 dtoverlay=rpi-sense 然后重启，刚刚上电的时候显示彩虹图，很快会熄灭，然后就可以正常使用了

## 0x 致谢

- [Sense HAT Doc.](https://pythonhosted.org/sense-hat/) 

- [python-sense-hat](https://github.com/astro-pi/python-sense-hat) by [astro-pi](https://github.com/astro-pi/)
