---
title: "Arduino:HID 库"
date: 2019-10-14T18:26:06+08:00
author: "An"
draft: false
toc: true
tags: 
  - Arduino
  - HID
---

![Cover](https://images.unsplash.com/photo-1560614220-60011c1d2139?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=100)

---

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
        server="netease"
        type="song"
        id="3407088">
</meting-js>

## 0x00 摘要

Arduino HID 库 **Keyboard** 与 **Mouse** 简单介绍

***「待完善」***

## 0x01 简介

`HID` 是 `Human Interface Device` 的缩写，由其名称可以了解HID设备是直接与人交互的设备，例如键盘、鼠标与游戏杆等。不过HID设备并不一定要有人机接口，只要符合HID类别规范的设备都是HID设备。

Arduino HID 库包含 ***Keyboard*** 与 ***Mouse*** 两个库，可分别模拟键盘与鼠标输入，由此可以特定硬件实现模拟键盘 **与/或** 鼠标执行特定操作

## 0x02 文档

### Keyboard

#### 说明

键盘功能使基于32u4或SAMD micro的板能够通过其micro的本机USB端口将击键发送到连接的计算机。

注意：并非所有可能的ASCII字符，特别是非打印的ASCII字符，都可以通过键盘库发送。
该库支持使用修饰键。同时按下修改键可以更改另一个键的行为。有关支持的键及其使用的其他信息，请参见此处

#### 注意和警告

这些核心库允许基于32u4和SAMD的主板（Leonardo，Esplora，Zero，Due和MKR系列）在连接的计算机上显示为本地鼠标和/或键盘。

使用鼠标和键盘库时要小心：如果鼠标或键盘库持续运行，将很难对您的电路板进行编程。如功能Mouse.move()和Keyboard.print()将光标移动或击键发送到相连的计算机，当你准备好来处理它们应该只被调用。建议使用控制系统打开此功能，例如物理开关或仅响应您可以控制的特定输入。有关一些解决方法，请参考“鼠标和键盘”示例。

使用鼠标或键盘库时，最好首先使用Serial.print（）测试输出。这样，您可以确保知道所报告的值。

#### 函数

##### Keyboard.begin()

###### 说明

与 [Arduino Leonardo](https://store.arduino.cc/usa/leonardo) 或 [Arduino Due](https://store.arduino.cc/usa/due) 一起使用时，`Keyboard.begin()` 开始模拟连接到计算机的键盘。要结束控制，请使用 `Keyboard.end()`

###### 语法

```cpp
Keyboard.begin()
```

###### 参数

无

###### 返回

无

##### Keyboard.end()

###### 说明

停止对连接的计算机的键盘仿真。要开始键盘仿真，请使用 `Keyboard.begin()` 。

###### 语法

```cpp
Keyboard.end()
```

###### 参数

无

###### 返回

无

##### Keyboard.press()

###### 说明

调用时，其 `Keyboard.press()` 功能就像在键盘上按住某个键一样。使用修饰键时很有用。要结束按键，请使用 `Keyboard.release()` 或 `Keyboard.releaseAll()`

###### 语法

```cpp
Keyboard.press(key)
```

###### 参数

`key` : 按下的键

允许的数据类型：`char`

###### 返回

发送的按键数

数据类型 : `size_t`

##### Keyboard.print()

###### 说明

将击键发送到连接的计算机

###### 语法

```cpp
Keyboard.print(character)
```

或

```cpp
Keyboard.print(characters)
```

###### 参数

`character` : 作为击键发送到计算机的字符或整数

`characters` : 将作为击键发送到计算机的字符串

###### 返回

发送的字节数

数据类型 : `size_t`

##### Keyboard.println()

###### 说明

将击键发送到连接的计算机，然后换行和回车

###### 语法

```cpp
Keyboard.println()
```

或

```cpp
Keyboard.println(character)
```

或

```cpp
Keyboard.println(characters)
```

###### 参数

`character` : 将作为击键发送给计算机的 `char`或 `int`，后跟换行符和回车符

`characters` : 作为击键发送到计算机的 `string`，后跟换行符和回车符

###### 返回

发送的字节数

数据类型 : `size_t`

##### Keyboard.release()

###### 说明

释放指定的键

###### 语法

```cpp
Keyboard.release(key)
```

###### 参数

`key` : 释放的键

允许的数据类型：`char`

###### 返回

释放的按键数

数据类型 : `size_t`

##### Keyboard.releaseAll()

###### 说明

释放当前按下的所有键

###### 语法

```cpp
Keyboard.releaseAll()
```

###### 参数

无

###### 返回

无

##### Keyboard.write()

###### 说明

将击键发送到连接的计算机。这类似于按下并释放键盘上的键。您可以发送一些ASCII字符或其他键盘修饰符和特殊键。

仅支持键盘上的ASCII字符。例如，ASCII 8（退格）将起作用，而ASCII 25（替代）则不起作用。发送大写字母时，Keyboard.write()发送移位命令和所需的字符，就像在键盘上键入一样。如果发送数字类型，则将其作为ASCII字符发送（例如，Keyboard.write（97）将发送“ a”）。

有关ASCII字符的完整列表，请参见ASCIITable.com

###### 语法

```cpp
Keyboard.write(character)
```

###### 参数

`character` : 要发送到计算机的字符或整数。可以以 `char` 可接受的任何符号发送

例如，以下所有内容均可接受，并发送相同的值65或ASCII A：

```cpp
Keyboard.write(65);         // sends ASCII value 65, or A
Keyboard.write('A');        // same thing as a quoted character
Keyboard.write(0x41);       // same thing in hexadecimal
Keyboard.write(0b01000001); // same thing in binary (weird choice, but it works)
```

###### 返回

发送的字节数

数据类型 : `size_t`

### Mouse

#### 说明

鼠标功能使基于32u4或SAMD micro的板能够通过其micro的本机USB端口控制所连接计算机上的光标移动。更新光标位置时，它始终相对于光标的先前位置。

#### 注意和警告

这些核心库允许基于32u4和SAMD的主板（Leonardo，Esplora，Zero，Due和MKR系列）在连接的计算机上显示为本地鼠标和/或键盘。

使用鼠标和键盘库时要小心：如果鼠标或键盘库持续运行，将很难对您的电路板进行编程。如功能Mouse.move()和Keyboard.print()将光标移动或击键发送到相连的计算机，当你准备好来处理它们应该只被调用。建议使用控制系统打开此功能，例如物理开关或仅响应您可以控制的特定输入。有关一些解决方法，请参考“鼠标和键盘”示例。

使用鼠标或键盘库时，最好首先使用Serial.print（）测试输出。这样，您可以确保知道所报告的值。

#### 函数

##### Mouse.begin()

###### 说明

开始模拟连接到计算机的鼠标。必须在控制计算机之前调用 `Mouse.begin()` 。要结束控制，请使用 `Mouse.end()`

###### 语法

```cpp
Mouse.begin()
```

###### 参数

无

###### 返回

无

##### Mouse.end

###### 说明

停止模拟连接到计算机的鼠标。要开始控制，请使用 `Mouse.begin()`

###### 语法

```cpp
Mouse.end
```

###### 参数

无

###### 返回

无

##### Mouse.click

###### 说明

在光标所在的位置向计算机发送瞬时单击。这与按下并立即释放鼠标按钮相同。

`Mouse.click()` 默认为鼠标左键

###### 语法

```cpp
Mouse.click()
```

或

```cpp
Mouse.click(button)
```

###### 参数

`button` : 要按下的鼠标按钮。

允许的数据类型 : `char`。

- `MOUSE_LEFT` （默认）

- `MOUSE_RIGHT`

- `MOUSE_MIDDLE`

###### 返回

无

##### Mouse.move

###### 说明

在连接的计算机上移动光标。屏幕上的运动始终相对于光标的当前位置

###### 语法

```cpp
Mouse.move(xVal, yVal, wheel)
```

###### 参数

`xVal`：沿x轴移动的量

允许的数据类型：`signed char`

`yVal`：沿y轴移动的量。

允许的数据类型：`signed char`

`wheel`：移动滚轮的数量。

允许的数据类型：`signed char`

###### 返回

无

##### Mouse.press

###### 说明

将按钮按下发送到连接的计算机。按下相当于单击并连续按住鼠标按钮。通过 `Mouse.release()` 释放按键。

`Mouse.press()` 默认为按下左键

###### 语法

```cpp
Mouse.press()
```

或

```cpp
Mouse.press(button)
```

###### 参数

`button` : 要按下的鼠标按钮。

允许的数据类型：`char`

- MOUSE_LEFT (默认)

- MOUSE_RIGHT

- MOUSE_MIDDLE

###### 返回

无

##### Mouse.release

###### 说明

发送一条消息，指出先前按下的按钮（通过 `Mouse.press()` 调用）已释放。`Mouse.release()` 默认为左键

###### 语法

```cpp
Mouse.release()
```

或

```cpp
Mouse.release(button)
```

###### 参数

`button` : 要释放的鼠标按钮。

允许的数据类型：`char`

- MOUSE_LEFT (默认)

- MOUSE_RIGHT

- MOUSE_MIDDLE

###### 返回

无

###### 注意和警告

使用该 `Mouse.release()` 命令时，Arduino将接管您的鼠标！使用命令之前，请确保您具有控制权。切换鼠标控制状态的按钮有效

##### Mouse.isPressed

###### 说明

检查所有鼠标按钮的当前状态，并报告是否按下任何鼠标按钮

###### 语法

```cpp
Mouse.isPressed()
```

或

```cpp
Mouse.isPressed(button)
```

###### 参数

没有传递任何值时，它将检查鼠标左键的状态

`button` : 要检查的鼠标按钮。

允许的数据类型：`char`

- MOUSE_LEFT (默认)

- MOUSE_RIGHT

- MOUSE_MIDDLE

###### 返回

报告是否按下按钮

数据类型：bool

## 0x03 引玉

***Keyboard*** 与 ***Mouse*** 有很多用途，但笔者觉得最有趣的应用，莫过于 ***BadUSB***，作为渗透测试的工具，从其原理上讲较难防范，笔者后续会详细介绍该类设备

## 0x04 致谢

- [Keyboard Doc](https://www.arduino.cc/reference/en/language/functions/usb/keyboard/)

- [Mouse Doc](https://www.arduino.cc/reference/en/language/functions/usb/mouse/)
