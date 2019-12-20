---
title: "Raspbian[Lite] 初始化"
date: 2019-10-27T16:30:23+08:00
author: "An"
draft: false
toc: true
tags: 
  - RaspberryPi
---

![Cover](https://images.unsplash.com/photo-1560872010-b2c30fbcd539?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

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

Raspbian[Lite] 初始化操作

***「待完善」***

## 0x01 简介

## 0x02 流程

### 启动前

#### 配置 WLAN

用户可以在未启动树莓派的状态下单独修改 `/boot/wpa_supplicant.conf` 文件配置 WiFi 的 *SSID* 和 *password* ，这样树莓派启动后会自行读取 wpa_supplicant.conf 配置文件连接 WiFi 设备。

在 boot 分区，也就是树莓派的 `/boot` 目录下编辑(新建) `wpa_supplicant.conf` 文件。以下为示例

```conf
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
ssid="WiFi-A"
psk="12345678"
key_mgmt=WPA-PSK
priority=1
}

network={
ssid="WiFi-B"
psk="12345678"
key_mgmt=WPA-PSK
priority=2
scan_ssid=1
}
```

P.S.

1.ssid : 网络的ssid
2.psk : 密码
3.priority:连接优先级，数字越大优先级越高（不可以是负数）
4.scan_ssid:连接隐藏WiFi时需要指定该值为1

- 如果 WiFi 没有密码

```conf
network={
ssid="ssid"
key_mgmt=NONE
}
```

- 如果 WiFi 使用WEP加密

```conf
network={
ssid="ssid"
key_mgmt=NONE
wep_key0="password"
}
```

- 如果 WiFi 使用WPA/WPA2加密

```conf
network={
ssid="ssid"
key_mgmt=WPA-PSK
psk="password"
}
```

#### 配置 SSH

Raspbian 默认 ssh 服务关闭

在 `boot` 分区新建一个文件，空白的即可，文件命名为 `ssh`。注意要小写且不要有任何扩展名。

>*Raspbian 默认用户*
>
>admin : pi
>
>password : raspberry

### 启动后

#### 更改密码

第一次启动系统后推荐更改 pi 用户密码

```bash
sudo passwd pi
```

#### 更改时区

Raspbian 默认时区为中时区 **(UTC)** ，需修改时区为东八区 **(UTC+8)**

```bash
sudo cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

#### 换源

##### Raspbian 源

>Raspbian 安装镜像和软件源

将 `/etc/apt/sources.list` 文件中默认的源地址 `http://raspbian.raspberrypi.org/` 替换为 `http://mirrors.ustc.edu.cn/raspbian/` 即可。

用如下命令替换：

```bash
sudo sed -i 's|raspbian.raspberrypi.org|mirrors.ustc.edu.cn/raspbian|g' /etc/apt/sources.list
```

##### Raspberrypi 源

>树莓派的 archive.raspberrypi.org 软件源，也即 **/etc/apt/sources.list.d/raspi.list** ，是由树莓派基金会提供的软件源，包括 ui 相关程序 ( 如 Raspbian 的桌面环境 PIXEL DE) 及部分由树莓派基金会为 树莓派编写的软件，通常与 **archive.raspbian.org** ( 参考 Raspbian 源使用帮助 ) 一起使用。

一般情况下，将 `/etc/apt/sources.list.d/raspi.list` 文件中默认的源地址 `http://archive.raspberrypi.org/` 替换为 `http://mirrors.ustc.edu.cn/archive.raspberrypi.org/` 即可。

用如下命令替换：

```bash
sudo sed -i 's|//archive.raspberrypi.org|//mirrors.ustc.edu.cn/archive.raspberrypi.org|g' /etc/apt/sources.list.d/raspi.list
```

##### 更新

```bash
sudo apt update && sudo apt upgrade
```

## 0x03 致谢

- [无屏幕和键盘配置树莓派WiFi和SSH](http://shumeipai.nxez.com/2017/09/13/raspberry-pi-network-configuration-before-boot.html) by [树莓派实验室](http://shumeipai.nxez.com/)

- [linux修改系统时间和linux查看时区、修改时区的方法](https://blog.csdn.net/zsg88/article/details/75212835) by [猪脚踏浪](https://me.csdn.net/zsg88)

- [Raspbian 源使用帮助](http://mirrors.ustc.edu.cn/help/raspbian.html) by [科大 LUG](https://lug.ustc.edu.cn/wiki/)

- [Raspberrypi 源使用帮助](http://mirrors.ustc.edu.cn/help/archive.raspberrypi.org.html) by [科大 LUG](https://lug.ustc.edu.cn/wiki/)
