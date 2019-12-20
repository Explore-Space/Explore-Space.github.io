---
title: "Unsplash"
date: 2019-07-03T20:42:01+08:00
author: "An"
draft: false
toc: true
tags: 
  - Unsplash
---

![Cover](https://images.unsplash.com/photo-1559275608-a600f8b7e110?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="29401226">
</meting-js>

## 0x00 摘要

关于Unsplash平台的想法

## 0x01 简介

>The internet’s source of freely useable images.  
>Powered by creators everywhere.

[![Unsplash](https://images.unsplash.com/moment-1544716590524-4fc5a168786e?dpr=3&auto=format&fit=crop&w=600&q=60 "Unsplash")](https://unsplash.com/)

## 0x02 决定

在此之前，笔者的照片并没有一个很好的归档方式：1.原始 JPG 和 RAW 定时上传到移动硬盘；2.筛选 JPG 在经过简单的后期处理后，上传至QQ空间、微信朋友圈、Instagram(由于上述平台上传照片时，均会极大地压缩照片画质到不可接受的程度，故目前已基本放弃上传至上述平台)；

笔者了解Unsplash平台大约是在2018年，那时并不能接受其[协议](https://unsplash.com/license)，同时客观来说，那时笔者所拍照片质量确实较低，故仅在该平台获取所需照片；

前不久，笔者觉得若不进行合理的归档整理，随着时间的推移，照片很可能会丢失。在权衡云端和本地两种归档方式后，笔者决定采用云端的方式整理照片。首先，考虑采用常规网盘，虽然国外平台无论从服务质量还是稳定性上都优于国内平台，但由于 GFW 的存在使得其几乎不可用，而国内平台的上传和下载限速严重，使其也几乎不可用；其次，考虑采用照片分享平台，国内的平台大多充斥着广告或捆绑其他东西，相对不那么“纯净”，而在国外的平台中笔者选中了规模较大的 Unsplash ；

笔者在认真思考后决定接受 Unsplash 协议。首先，笔者目前并没有照片商业化的需求，而且客观来说，目前所拍的照片并没有商业价值；其次，正是在该协议下，笔者也受益很大，笔者逐渐接受并喜欢这样“开源”的平台。

## 0x03 迁移

- [MyUnsplash](https://unsplash.com/@explore_)

笔者在本地的备份文件中筛选有价值的照片，然后进行简单的后期处理。这一过程是比较耗时的，虽然笔者拍的照片时间跨度(2018.07 ~ 2019.06)和数量都不大，但无论是在前期筛选还是后期调整过程中都面临很多抉择。

笔者开始将照片上传到 Unsplash 后，首先面临的便是上传数量限制 10张/周 ，笔者的照片虽然不多，但算下来至少需要5周左右才能将目前的库存照片上传完，但出乎笔者的意料，在 2019.06.23(注册：2019.06.01) Unsplash 管理团队发送邮件告知解除了笔者上传数量的限制，照片被认可的感觉让笔者很高兴。

- 邮件:

>From: "Annie from Unsplash"<delivery@unsplash.com>  
>Date: 2019/6/23 15:32:40  
>To: My E-mail  
>Subject: Next level Unsplash unlocked  
>>Annie here  <br/> 
>>Just wanted to let you know that we've been liking your recent submissions so much that we've removed your weekly upload limit on your account!  <br/> 
>>Thanks you for contributing such awesome photos to the Unsplash community and for being part of the Unsplash family.  <br/> <br/> 
>>Annie  
>>Head of Editorial  
>>@unsplash

## 0x04 扩展

### 背景

Unsplash中的图片主要有两种下载方式:常规下载和API下载。常规下载虽没有数量限制，但效率较低；官方提供的API在程序Demo阶段有[速度限制](https://unsplash.com/documentation#rate-limiting) 50张/h ，故也几乎不可用。

### 实现

#### 分析网站

在API文档中，发现有个[List Collections](https://unsplash.com/documentation#list-photos)功能，用JSON的格式返回照片列表。该API的GET的参数有page，per_page。尝试枚举，发现最大的per_page(每页显示的照片数量)为30张，page(页码)最大值为4067(截止至 2019-07-05 10:00:00)，所以整站大概有 122K 张摄影作品。

Unsplash推出了一款名为[Unsplash Instant](https://instant.unsplash.com/?utm_campaign=api-feature&utm_medium=referral&utm_source=unsplash)的Chrome插件

安装完成后尝试寻找保存在插件中的Public Key，发现其保存在了插件目录下的js\main.js文件中。虽然JS代码经过压缩，但并不难找。其官方的Client_ID为：

```text
fa60305aa82e74134cabc7093ef54c8e2c370c47e73152f72371c828daedfcd7
```

最终得到网站api为:

```text
https://api.unsplash.com/photos/?client_id=fa60305aa82e74134cabc7093ef54c8e2c370c47e73152f72371c828daedfcd7&page=1&per_page=30
```

其中page, per_page在爬取时修改

访问api地址,可得到包含图片url的json , 包括种类raw, full, regular, small, thumb. 最终取raw

#### Scrapy实现

(省略)

#### 多线程下载器

(省略)

### 源码

[UnsplasDownload](https://github.com/Explore-Space/UnsplashDownload)

### Todo

[ ] 重构 download.py

### 致谢

- [写只爬虫，把Unsplash的2W摄影素材扒个精光](https://zhuanlan.zhihu.com/p/24855089)

- [python-Scrapy爬取unsplash美图(壁纸)](https://blog.csdn.net/baidu_21802103/article/details/81147050)

## 0x05 尾巴

随着时间的推移，笔者渐渐的接受并追求“开源”平台，“开源”也逐渐成为笔者的人生信条。

>我期待一个完全开源的世界
