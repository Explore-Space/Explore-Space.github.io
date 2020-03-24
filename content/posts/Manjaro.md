---
title: "Manjaro:KDE"
date: 2019-09-16T23:31:18+08:00
author: "An"
draft: false
toc: true
tags: 
  - Linux
  - Manjaro
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
        id="27759600">
</meting-js>

## 0x00 摘要

Manjaro 的安装与配置

## 0x01 起源

在看过[TheCW](https://space.bilibili.com/13081489)的系列视频后，被其使用的 Linux 发行版 [Manjaro](https://www.manjaro.org/) 深深的吸引，更精致的外观，更优雅的操作。

笔者从接触 Linux 到现在，一直在使用 Debian 及其衍生发行版

- [Debian](https://www.debian.org/)
- [Ubuntu](https://ubuntu.com/)
- [Deepin](https://www.deepin.org/)
- [Raspbian](https://www.raspberrypi.org/downloads/raspbian/)
- [Armbian](https://www.armbian.com/)
- [Kali](https://www.kali.org/)
- [ParrotSec](https://parrotlinux.org/)

## 0x02 安装

### 前

#### 获取镜像

ISO可从镜像站获取 ([USTC](https://mirrors.ustc.edu.cn/), [Aliyun](https://opsx.alibaba.com/mirror?lang=zh-CN), [Tsinghua](https://mirrors.tuna.tsinghua.edu.cn) , etc)

#### 烧录镜像

烧录镜像可用 [BalenaEtcher](https://www.balena.io/etcher/) 。开源，易用，优雅(当然 dd 命令更优雅，但无奈总是记不住参数)

![界面](/Image/posts/Manjaro/001.png)

### 中

#### 语言

安装中选择语言为英语，若选择中文， `/home/□□□□□/` 目录中的文件为中文名，即 `Desktop` , `Documents` , `Downloads` , `Music` , `Pictures` , `Public` , `Templates` , `Videos` 文件夹为对应中文，会使在终端中操作文件较为复杂

### 后

#### 禁用独显

在安装完成后，立即重启会进入假死状态，需要强制重启。在 BIOS 启动后，进入系统前，按 *Esc* 进入 grub 选择界面，按 *E* 编辑 grub ，在 quiet 后插入 `nouveau.modeset=0` ，按 *F10* 或 *Ctrl* + *X* 保存后即可正常启动

启动后修改 grub 配置文件，默认禁用独显(后文会详述独显驱动安装，该处为方便暂时只用核显)。修改 `/etc/default/grub` 同上

更新 grub 配置

```bash
sudo update-grub
```

#### 更改语言

在 `System Settings` - `Locale` 中双击 *中文(中国)* ，使 *Display Language* 与 *Formats* 选至 *中文(中国)* 即可，保存

修改前

![修改前](/Image/posts/Manjaro/002.png)

修改后

![修改后](/Image/posts/Manjaro/003.png)

重启后生效

#### 配置软件源

##### Manjaro源

生成可用中国镜像站列表，根据实际网络情况选择合适镜像源 (笔者一般首选 USTC 和 Aliyun 镜像站，但目前 Aliyun 没有 Manjaro 镜像，故选择 USTC)

```bash
sudo pacman-mirrors -i -c China -m rank
```

执行更新(选择项全部默认即可)

```bash
sudo pacman -Syyu
```

##### Arch Linux CN源

>简介
>
>Arch Linux 中文社区仓库是由 Arch Linux 中文社区驱动的非官方用户仓库。包含中文用户常用软件、工具、字体/美化包等。

在 `/etc/pacman.conf` 文件末尾添加两行：

```conf
[archlinuxcn]
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```

然后安装 `archlinuxcn-keyring` 包以导入 GPG key

```bash
sudo pacman -Sy archlinuxcn-keyring
```

#### 常用软件安装

##### yay

```bash
sudo pacman -Sy yay
```

##### QQ

```bash
yay -Sy linuxqq
```

##### 中文输入法

- 安装

```bash
sudo pacman -Sy fcitx-im fcitx-configtool fcitx-googlepinyin
```
  
- 在 `~/.xprofile` 中添加以下内容

```text
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=”@im=fcitx”
```

P.S. 笔者习惯用Google输入法，若习惯搜狗拼音，可将上述命令中 `fcitx-googlepinyin` 替换为 `fcitx-sougoupinyin`

##### WPS

- 安装

```bash
sudo pacman -Sy wps-office ttf-wps-fonts
```

- 解决无法输入中文问题，分别在 `/usr/bin/wps` (Word), `/usr/bin/et` (Excel), `/usr/bin/wpp`(PowerPoint) 中第2行添加以下内容

```text
export XMODIFIERS="@im=fcitx"
export QT_IM_MODULE="fcitx"
```

##### Chrome 浏览器

```bash
sudo pacman -Sy google-chrome
```

##### uGet && aria2

```bash
sudo pacman -Sy uget aria2
```

##### Neovim

```bash
sudo pacman -Sy neovim
```

P.S. 笔者习惯于 Neovim，若习惯于 Vim 可将上述命令中 `neovim` 替换为 `vim`

##### Postman

```bash
sudo pacman -Sy postman-bin
```

##### Visual Studio Code

```bash
sudo pacman -Sy visual-studio-code-bin
```

##### BalenaEtcher

```bash
sudo pacman -Sy etcher
```

##### Oh My Zsh

- via curl

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

- via wget

```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

P.S.

1.Manjaro 中已安装 zsh ，故只需安装 oh-my-zsh 即可
2.在 oh-my-zsh 安装过程中，会设置 Zsh 为默认 shell

##### Ranger

```bash
sudo pacman -Sy ranger
```

##### GIMP

```bash
sudo pacman -Sy gimp
```

##### 网易云第三方客户端

```bash
sudo pacman -Sy electron-netease-cloud-music
```

P.S. 笔者习惯该客户端，如需官方客户端只需将 `electron-netease-cloud-music` 替换为 `netease-cloud-music`

##### Arduino IDE

```bash
sudo pacman -Sy arduino
```

##### Cmake

```bash
sudo pacman -Sy cmake
```

#### 配置双显卡驱动

- 安装依赖

```bash
sudo pacman -Sy virtualgl lib32-virtualgl lib32-primus primus
```

- 安装nvidia闭源驱动与intel驱动混合版bumblebee

系统设置 - 硬件设定 - Display controller 中，安装 `video-hybrid-intel-nvidia-□□□□□-bumblebee`

P.S. □□□□□ 为版本号，笔者目前所用版本号为 430xx

>**存疑**
>
>安装nvidia闭源驱动与intel驱动混合版bumblebee
>
>sudo mhwd -f -i pci video-hybrid-intel-nvidia-bumblebee
>
>在安装“video-hybrid-intel-nvidia-bumblebee”这个步骤的时候，先用mhwd命令查看安装的名字，会出现如"video-hybrid-intel-nvidia-430xx-bumblebee"这样的名字，选一个安装

- 开启自动启动bumblebeed服务

```bash
sudo systemctl enable bumblebeed
```

- 将用户添加到bumblee组

```bash
sudo gpasswd -a $USER bumblebee
```

- 配置 grub
  
修改 `/etc/default/grub` 在 `quiet` 后添加以下内容

```text
acpi_osi=! acpi_osi=’Windows 2009’
```

或者

```text
acpi_osi=! acpi_osi=Linux acpi_osi=’Windows 2015’ pcie_port_pm=off
```

>**存疑**
>
>理由如下:
>很多硬件厂商的BIOS驱动都对Linux不友好，无法顺利加载ACPI模块，而导致无法驱动独立显卡,acpi_osi=’Windows 2009’的意思是告诉ACPI模块，我是‘Windows 7’，别闹情绪了，赶紧工作吧。

- 更新 grub 配置

```bash
sudo update-grub
```

- 重启

```bash
reboot
```

- 测试
  
  - 测试集显性能
  
  ```bash
  glxgears
  ```

  - 测试独显性能
  
  ```bash
  optirun glxgears
  ```

  - 查看独显信息
  
  ```bash
  optirun nvidia-smi
  ```

P.S. 如需以独立显卡运行某软件，需在指令前加 `optirun` 。如以独显运行 Chrome 浏览器，需执行以下命令

```bash
optirun google-chrome-stable
```

#### 编程环境配置

##### Nodejs && npm

- 安装

  ```bash
  sudo pacman -Sy npm
  ```
  
  P.S. 安装 npm 过程中会自动安装 nodejs

- 换源

  ```bash
  npm config set registry https://registry.npm.taobao.org
  ```

  验证

  ```bash
  npm config list
  ```

##### PyPI

- 安装

Manjaro 中自带有 pip(For Python 2) 与 pip3(For Python 3)，无需手动安装

- 换源

  - 常规
    编辑 `$HOME/.config/pip/pip.conf` (若 `.config` 目录中，不存在 `pip` 文件夹，创建即可)

    `pip.conf` 文件配置示例如下：

    ```conf
    [global]
    index-url = https://mirrors.aliyun.com/pypi/simple/
    ```

  - P.S.

    1.笔者的网络环境下，阿里云镜像源速度与稳定性相对较好，可根据自己的网络环境自行选择，笔者列出几个相对稳定的镜像源

    >阿里云  `https://mirrors.aliyun.com/pypi/simple/`
    >
    >中国科技大学  `https://pypi.mirrors.ustc.edu.cn/simple/`
    >
    >清华大学  `https://pypi.tuna.tsinghua.edu.cn/simple/`
    >
    >豆瓣  `https://pypi.douban.com/simple/`

    2.上述的常规配置中，仅对当前用户有效，若需要全局配置，则修改 `/etc/pip.conf` 同上

#### 非常用软件安装

##### STM32CubeMX

- 简介

 >STM32CubeMX is a graphical tool that allows a very easy configuration of STM32 microcontrollers and microprocessors, as well as the generation of the corresponding initialization C code for the Arm® Cortex®-M core or a partial Linux® Device Tree for Arm® Cortex®-A core), through a step-by-step process.

- 安装

```bash
yay -Sy stm32cubemx
```

##### STM32CubeIDE && J-Link

- 简介

>STM32CubeIDE is an advanced C/C++ development platform with IP configuration, code generation, code compilation, and debug features for STM32 microcontrollers.
>
>STM32 CuBeIDE是一种先进的C/C++开发平台，具有STM32微控制器的IP配置、代码生成、代码编译和调试功能。

- 安装

  1.下载 STM32CubeIDE 到 `~/Downloads`

  [STM32CubeIDE](https://www.stmcu.com.cn/Designresource/design_resource_detail?file_name=STM32CubeIDE_Lnx_STM33%E9%9B%86%E6%88%90%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83&lang=EN&ver=1.0.2)

  2.重命名`STM32CubeIDE_Lnx_V1.0.2.zip` 为 `en.st-stm32cubeide_1.0.2_3566_20190716_0927_amd64.sh.zip`

  3.执行安装

  ```bash
  yay -Sy stm32cubeide
  ```

- P.S.
  
  1.步骤1中，通过 **yay** 安装部分软件时，需要自行下载软件包， yay 会自动检测 **Downloads** 目录是否存在该文件

  2.步骤2中，更改文件名端目的是，在 STM32CubeIDE 安装脚本中检测的文件名为特定形式。其中 **版本号** 与 **日期**  需要根据实际情况更改 (*可先执行步骤3,查看报错信息，然后根据提示替换步骤2中版本号与日期*)

##### DaVinci Resolve

- 简介

>DaVinci Resolve 16 is the world’s only solution that combines professional 8K editing, color correction, visual effects and audio post production all in one software tool!
>
>达芬奇16是世界上唯一的解决方案，结合专业8K编辑，色彩校正，视觉效果和音频后期制作在一起的软件工具！

- 安装

  1.下载 DaVinciResolve 到 `~/Downloads`

  [DaVinciResolve](http://www.blackmagicdesign.com/cn/products/davinciresolve/)

  2.执行安装

  ```bash
  yay -Sy davinci-resolve
  ```

  3.更改配置

  右键 DaVinci Resolve 图标，选择编辑应用程序，修改 应用程序 - 命令 `/opt/resolve/bin/resolve` 为 `optirun /opt/resolve/bin/resolve`

- P.S.
  
  1.步骤1中，通过 **yay** 安装部分软件时，需要自行下载软件包， yay 会自动检测 **Downloads** 目录是否存在该文件

  2.步骤3中，更改命令的目的是，在安装完双显卡混合驱动后，会默认以核显运行程序，以独显执行命令需在命令前添加 `optirun` 。以核显运行 DaVinciResolve 在初始配置完成后，会出现闪退现象，故需以独显运行 DaVinciResolve

## 0x03 FAQ

### Manjaro 中文显示方块

在升级系统后可能出现这个问题

解决：

```bash
sudo pacman -S wqy-microhei
```

## 0x04 趣闻

### 更新

![趣闻_1](/Image/posts/Manjaro/004.jpg)

这张图可以说很真实了，2333,笔者每次开机第一件事便是 `sudo pacman -Syyu`

### ”滚炸“

![趣闻_2](/Image/posts/Manjaro/005.jpg)

由于 Arch Linux 滚动更新的特性，所以每次升级都伴随着风险，常常可以看到抱怨 Arch Linux “滚炸”的，可能会出现各种各样的问题，2333，但到目前为止，笔者还没遇到"滚炸"的情况

## 0x05 致谢

- [Manjaro Linux 源使用帮助](http://mirrors.ustc.edu.cn/help/manjaro.html) by [科大 LUG](https://lug.ustc.edu.cn/wiki/)

- [Arch Linux CN 源使用帮助](http://mirrors.ustc.edu.cn/help/archlinuxcn.html) by [科大 LUG](https://lug.ustc.edu.cn/wiki/)

- [PyPI 镜像源使用帮助](http://mirrors.ustc.edu.cn/help/pypi.html) by [科大 LUG](https://lug.ustc.edu.cn/wiki/)

- [Manjaro常用软件和命令行推荐](https://blog.csdn.net/was172/article/details/82826607) by [was172](https://blog.csdn.net/was172)

- [Manjaro Linux 配置Intel与Nvidia双显卡切换](https://mtaoist.me/2018/03/19/Bumblebee/) by [taoist](https://mtaoist.me/)
