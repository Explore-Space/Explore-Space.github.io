---
title: "折腾日志 :网络"
date: 2019-07-22T23:22:52+08:00
author: "An"
draft: false
toc: true
tags: 
  - 折腾日志
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
        id="19945735">
</meting-js>

## 0x00 摘要

记录折腾网络(移动光纤)的过程

## 0x01 背景

搬校区后，只有交通和网络这两点有所改善，小区宽带运营商只有移动和联通，价格差异不大，都是 700+ 元 / (100M * 年)，笔者看了下入户段情况:联通4芯网线，移动光纤，故选择移动。

以笔者的路由器做二级路由，5.8 G WIFI 和有线连接测速峰值为 150 Mbps 左右，比理论略高，现目前笔者所在小区人极少，之后全部入住后速度应该会有所下降( 后来这一想法得以验证 )。

这里忍不住吐槽一下移动自带的光猫:1. 单频段 WIFI ；2. 只有1个 1000M LAN ，其余为 100M LAN

## 0x02 折腾

笔者的路由器仅做二级路由 ，有所浪费，开始折腾。

### 1.思路

- 将光猫 **(型号:H1S-3 以下记作 H1S-3)** 从路由模式转换为桥接模式
- 由路由器 **(型号:K2P 以下记作 K2P)** 进行PPPOE拨号
- 尝试单线多拨
- 尝试 SS/SSR

### 2.过程

#### 更改 H1S-3 模式

笔者通过默认 `user` 用户，进入 H1S-3 Web 控制台并没有看到相关选项，便开始查找，很快便找到结果了: 默认的user用户只有很小部分控制权，超级用户才有完整权限。笔者找到了超级用户的账号和密码

>admin: CMCCAdmin <br/> password: aDm8H%MdA

P.S. 该帐号其实是通过下文的操作获取的，为方便操作，笔者直接展示结果

>**存疑**
>
>该帐号与密码应该具有普适性

#### 准备PPPOE账号及密码

##### 已知

安装时，可向安装人员索要

P.S. 笔者所在地区的移动宽带的默认密码为帐号后6位

##### 未知

###### 方案1

可通过拨打运营商服务电话获取密码

###### 方案2

- 思路:
  - 打开 H1S-3 **Telnet** 端口
  - 通过 Telnet 连接H1S-3
  - 在配置文件中找到PPPOE账号及密码

- 实现

  1. 打开 H1S-3 Telnet 端口

  工具: Firefox 浏览器，HTTPHeader Live 插件
  
  使用 user 用户登陆 H1S-3 Web 控制台，打开HTTP Header Live插件，在页面上随便点击一个页面，在HTTP Header Live插件中捕捉到了post信息

  打开一个post，修改链接为:

  ```text
  http://192.168.1.1/boaform/set_telenet_enabled.cgi
  ```

  修改内容为:

  ```text
  mode_name=set_telenet_enabled&nonedata=0.3535281170047305&user_name=root&user_password=admin&telenet_enabled=1&default_flag=1
  ```

  然后点击右下角的“send”，会返回一个成功的页面，代表已经成功打开打开 H1S-3 Telnet 端口
  
  2. 通过 Telnet 连接H1S-3
  
  For Windows(CMD):

  ```bash
  Telnet 192.168.1.1
  ```

  For Ubuntu:

  ```bash
  telnet 192.168.1.1
  ```

  >admin:  root  <br /> password:  admin

  登录成功后:

  3. 在配置文件中找到PPPOE账号及密码

  ```bash
  more /config/worka/backup_lastgood.xml
  ```

#### 尝试单线多拨

在多次尝试后，最多能以4拨实现约 400 Mbps ，效果比较理想

但目前尚不清楚现有架构中瓶颈在哪，笔者觉得很大可能在硬路由，日后有机会组1台软路由再折腾

![多拨测速](/Image/posts/Network_1/001.jpg)

#### 尝试 SS/SSR

很无奈的是，笔者目前并没有找到一个多拨与 SS/SSR 可以兼顾的 K2P 固件，通过刷写不同固件可分别两项功能。在综合考虑后，笔者选择实现单线多拨，摒弃 SS/SSR

---
---
---

## 0x03 继续

开学全部入住后，网速有明显下降。笔者在纠结很久后终于下定决心，购买软路由，希望能够改善网络情况。

在接入软路由后，进行多拨，网速有明显提高

![多拨测速](/Image/posts/Network_1/002.jpg)

软路由的开放性更高，后续可能会详细写相关专题

## 0x04 致谢

- [中国移动H1S-3光猫首发破解教程](https://tieba.baidu.com/p/5931041933?pid=122636821539&cid=0&red_tag=3414956069#122636821539) by [cq5683130]()

- [学了改移动H1S-3光猫为桥接，感恩的发个感谢攻略](https://tieba.baidu.com/p/5986259213?red_tag=1562136839) by [shymedia]()

- [恩山无线论坛](https://www.right.com.cn/forum/)
