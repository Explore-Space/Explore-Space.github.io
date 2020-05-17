---
title: "Primitive"
date: 2019-12-24T22:31:18+08:00
author: "An"
draft: false
toc: true
tags: 
  - Blog
  - Github Actions
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
        id="27759600">
</meting-js>

## 0x00 摘要



## 0x01 起源

![000](/Image/posts/Primitive/000_000.gif)

![000](/Image/posts/Primitive/000.jpeg)

## 0x02 运行

### 安装Go

具体安装配置流程可参考[官方文档](https://golang.org/doc/install)

### 运行primitive

```go
go get -u github.com/fogleman/primitive
```

```bash
primitive -i input.png -o output.png -n 100
```



## 0x04 致谢

- [primitive](https://github.com/fogleman/primitive) by [fogleman](https://github.com/fogleman)