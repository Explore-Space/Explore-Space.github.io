---
title: "Markdown"
date: 2018-12-09T18:00:00+08:00
author: "An"
draft: false
toc: true
tags: 
  - Markdown
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
        id="5113327">
</meting-js>

## 0x00 摘要

简述Markdown基本操作

## 0x01 前言

在笔者搭建Blog之前，一直以为其中的文章都要像写前端那样写，心中不由觉得很麻烦。后来才了解到Markdown语言，很快笔者就能熟练的用Markdown直接写Blog了，其功能性与简洁性恰巧处于平衡点。

## 0x02 简介

>[Markdown](https://en.wikipedia.org/wiki/Markdown) is a lightweight markup language with plain text formatting syntax. Its design allows it to be converted to many output formats, but the original tool by the same name only supports HTML. Markdown is often used to format readme files, for writing messages in online discussion forums, and to create rich text using a plain text editor. Since the initial description of Markdown contained ambiguities and unanswered questions, the implementations that appeared over the years have subtle differences and many come with syntax extensions.
>
>Markdown 是一种具有纯文本格式语法的轻量级标记语言。它的设计允许将其转换为多种输出格式，但原来同名的工具只支持html。标记通常用于格式化自述文件、在在线论坛中编写消息以及使用纯文本编辑器创建富文本。由于最初对标记的描述包含含糊不清和未回答的问题，多年来出现的实现有微妙的差异，许多都带有语法扩展

## 0x03 语法

### 标题

#### 规则

在想要设置为标题的文字前面加#来表示.一个#是一级标题，二个#是二级标题,以此类推.支持六级标题。

#### 示例

```text
# 一级标题
## 二级标题
### 三级标题
```

#### 效果

(省略)

### 字体

#### 规则

- **加粗**:加粗的文字左右分别用两个 * 包起来

- *斜体*:倾斜的文字左右分别用一个 * 包起来

- ***斜体加粗***:倾斜和加粗的文字左右分别用三个 * 包起来

- ~~删除线~~:加删除线的文字左右分别用两个 ~ 包起来

#### 示例

```text
**加粗**
*斜体*
***斜体加粗***
~~删除线~~
```

#### 效果

**加粗**
*斜体*
***斜体加粗***
~~删除线~~

### 引用

#### 规则

在引用的文字前加 > 即可。引用也可以嵌套，层数不限制。

#### 示例

```text
>引用1
>>引用2
>>>引用3
>>>>引用4
```

#### 效果

>引用1
>>引用2
>>>引用3
>>>>引用4

### 分割线

#### 规则

三个或者三个以上的 - 或者 * 都可以.

#### 示例

```text
---
----
***
****
```

#### 效果

---
----
***
****

### 图片

#### 规则

```markdown
![alt](图片地址 ''title'')
```

- alt:显示在图片下面的文字，相当于对图片内容的解释。
- title:图片的标题，当鼠标移到图片上时显示的内容，该参数可选

#### 示例

```markdown
![GitHub](/Image/posts/Markdown-α/001.jpeg "Git")
```

#### 效果

![GitHub](/Image/posts/Markdown-α/001.jpeg "Git")

### 超链接

#### 规则

```markdown
[alt](超链接地址 "超链接title")
```

- alt:显示的文字，相当于超链接名。
- title:超链接的标题，当鼠标移到超链接上时显示的内容，该参数可选

#### 示例

```markdown
[GitHub](https://github.com/)
[GitLab](https://about.gitlab.com/ "Title")
```

#### 效果

[GitHub](https://github.com/)
[GitLab](https://about.gitlab.com/ "Title")

### 列表

#### 无序列表

##### 规则

在无序列表内容前加 - + * 任何一种

##### 示例

```markdown
- 无序列表1
+ 无序列表2
* 无序列表3
```

##### 效果

- 无序列表1
+ 无序列表2
* 无序列表3

#### 有序列表

##### 规则

在有序列表内容前加数字加点

##### 示例

```markdown
1.有序列表1
2.有序列表2
3.有序列表3
```

##### 效果

1.有序列表1
2.有序列表2
3.有序列表3

#### 列表嵌套

##### 规则

上一级和下一级之间敲三个空格即可

##### 示例

```markdown
- 一级无序列表1
   + 二级无序列表1
   - 二级无序列表2
+ 一级无序列表2
   1. 二级有序列表1
   2. 二级有序列表2
1. 一级有序列表1
   + 二级无序列表1
   - 二级无序列表2
2. 一级有序列表2
   1. 二级有序列表1
   2. 二级有序列表2
```

##### 效果

- 一级无序列表1
  + 二级无序列表1
  - 二级无序列表2

+ 一级无序列表2
  1. 二级有序列表1
  2. 二级有序列表2

1. 一级有序列表1
  + 二级无序列表1
  - 二级无序列表2

2. 一级有序列表2
  1. 二级有序列表1
  2. 二级有序列表2

### 表格

#### 规则

```markdown
表头|表头|表头
-|-|-
内容|内容|内容
内容|内容|内容
```

1. |、-、:之间的多余空格会被忽略，不影响布局。
2. 默认标题栏居中对齐，内容居左对齐。
3. -:表示内容和标题栏居右对齐，:-表示内容和标题栏居左对齐，:-:表示内容和标题栏居中对齐。
4. 内容和|之间的多余空格会被忽略，每行第一个|和最后一个|可以省略，-的数量至少有一个。

#### 示例

```markdown
表头1|表头2|表头3
-|-|-
(1,1)|(1,2)|(1,3)
(2,1)|(2,2)|(2,3)
(3,1)|(3,2)|(3,3)
```

#### 效果

表头1|表头2|表头3
-----|:--:|-----:
(1,1)|(1,2)|(1,3)
(2,1)|(2,2)|(2,3)
(3,1)|(3,2)|(3,3)

### 代码

#### 单行代码

##### 规则

代码之间分别用一个反引号包起来

##### 示例

```markdown
`Hello World!`
```

##### 效果

`Hello World!`

#### 代码块

##### 规则

代码之间分别用三个反引号包起来，且两边的反引号单独占一行

##### 示例

```markdown
` * 3
package main  //Golang
import "fmt"
func main(){
fmt.Println("Hello World !")
}
` * 3
```

##### 效果

```go
package main  //Golang
import "fmt"
func main(){
fmt.Println("Hello World !")
}
```

#### 通用

##### 规则

每行代码前缩进四个空格

##### 示例

(省略)

##### 效果

```python
print('Hello World!')  #Python3
```

### 流程图

#### 示例

```markdown
` * 3 flow
st=>start: 开始
op=>operation: My Operation
cond=>condition: Yes or No?
e=>end
st->op->cond
cond(yes)->e
cond(no)->op
& ` * 3
```

#### 效果

略

(注:由于 Blog 目前所使用 Markdown 中不支持流程图)

## 0x04 致谢

- [Markdown基本语法](https://www.jianshu.com/p/191d1e21f7ed) by [高鸿祥](https://www.jianshu.com/u/1f5ac0cf6a8b)

- [Markdown 教程](https://www.runoob.com/markdown/md-tutorial.html) by [菜鸟教程](https://www.runoob.com/)

## 0x05 尾巴

Markdown能极大地简化文档书写，相比 Word ，使用 Markdown 可以专注于内容，而非无关紧要但繁杂的格式问题。
