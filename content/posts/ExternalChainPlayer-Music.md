---
title: "外链播放器:音乐"
date: 2019-10-18T17:47:13+08:00
author: "An"
draft: false
toc: true
tags: 
  - Blog
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
        id="30953009">
</meting-js>

## 0x00 摘要

关于音乐外链播放器

***「持续更新」***

## 0x01 简介

从前，在自己的 Blog 中插入外链音乐播放器很容易，[网易云音乐](https://music.163.com/)等等平台会有专门的外链播放器生成通道，复制粘贴就可以，直到...

![001](/Image/posts/ExternalChainPlayer-Music/001.png)

但笔者找到了很棒的解决方案

***「[MetingJS](https://github.com/metowolf/MetingJS)」***

![002](/Image/posts/ExternalChainPlayer-Music/002.png)

>A powerful plugin connect APlayer and Meting
>
>一个连接 APlayer 和 Meting 强大的插件

## 0x02 使用

### 快速开始

#### A

***`https://music.163.com/#/playlist?id=60198`***

##### 代码

```html
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="playlist"
        id="60198">
</meting-js>
```

##### 实例

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="playlist"
        id="60198">
</meting-js>

#### B

***`https://y.qq.com/n/yqq/song/001RGrEX3ija5X.html`***

##### 代码

```html
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        auto="https://y.qq.com/n/yqq/song/001RGrEX3ija5X.html">
</meting-js>
```

##### 实例

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        auto="https://y.qq.com/n/yqq/song/001RGrEX3ija5X.html">
</meting-js>

#### C

***for self-hosted media***

***对于自托管媒体***

##### 代码

```html
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        name="rainymood"
        artist="rainymood"
        url="https://rainymood.com/audio1110/0.m4a"
        cover="https://rainymood.com/i/badge.jpg">
</meting-js>
```

##### 实例

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        name="rainymood"
        artist="rainymood"
        url="https://rainymood.com/audio1110/0.m4a"
        cover="https://rainymood.com/i/badge.jpg">
</meting-js>

#### D

***Fixed mode with Lyric text***

***歌词文本固定模式***

##### 代码

```html
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        name="rainymood"
        artist="rainymood"
        url="https://rainymood.com/audio1110/0.m4a"
        cover="https://rainymood.com/i/badge.jpg"
        fixed="true">
        <pre hidden>
                [00:00.00]This
                [00:04.01]is
                [00:08.02]lyric
        </pre>
</meting-js>
```

##### 实例

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        name="rainymood"
        artist="rainymood"
        url="https://rainymood.com/audio1110/0.m4a"
        cover="https://rainymood.com/i/badge.jpg"
        fixed="false">
        <pre hidden>
                [00:00.00]This
                [00:04.01]is
                [00:08.02]lyric
        </pre>
</meting-js>

### 选项

|option          |default       |description|
|:---------------|:------------:|:----------|
|id              |**require**   |song id / playlist id / album id / search keyword|
|server          |**require**   |music platform: `netease`, `tencent`, `kugou`, `xiami`, `baidu`|
|type            |**require**   |`song`, `playlist`, `album`, `search`, `artist`|
|auto            |options       |music link, support: `netease`, `tencent`, `xiami`|
|fixed           |`false`       |enable fixed mode|
|mini            |`false`       |enable mini mode|
|autoplay        |`false`       |audio autoplay|
|theme           |`#2980b9`     |main color|
|loop            |`all`         |player loop play, values: 'all', 'one', 'none'|
|order           |`list`        |player play order, values: 'list', 'random'|
|preload         |`auto`        |values: 'none', 'metadata', 'auto'|
|volume          |`0.7`         |default volume, notice that player will remember user setting, default volume will not work after user set volume themselves|
|mutex           |`true`        |prevent to play multiple player at the same time, pause other players when this player start play|
|lrc-type        |`0`           |lyric type|
|list-folded     |`false`       |indicate whether list should folded at first|
|list-max-height |`340px`       |list max height|
|storage-name    |`metingjs`    |localStorage key that store player setting|

## 0x 致谢

- [MetingJS](https://github.com/metowolf/MetingJS) by [metowolf](https://github.com/metowolf)

- [APlayer](https://github.com/MoePlayer/APlayer) by [MoePlayer](https://github.com/MoePlayer)

- [音乐网站都不提供外链播放器，是有什么特别的考虑吗？](https://www.v2ex.com/amp/t/559189) by [V2EX](https://www.v2ex.com/)
