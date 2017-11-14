---
layout:     post
title:      "1 bit ALU 设计流程概览"
subtitle:   "展示利用IP核进行ALU设计，烧写和封装"
date:       2017-11-13 14:00:00
author:     "Sirius"
header-img: "img/ALU-BANNER.jpg"
tags:
    - 数字电路
    - 实验
    - Vivado
---
# ALU 设计流程概览

<!-- TOC -->

- [ALU 设计流程概览](#alu-设计流程概览)
    - [环境说明](#环境说明)
    - [新建工程](#新建工程)
    - [导入IP核](#导入ip核)
    - [画电路图](#画电路图)
        - [根据 ALU 功能表写出真值表](#根据-alu-功能表写出真值表)
        - [根据真值表构建电路图](#根据真值表构建电路图)
    - [仿真](#仿真)
        - [修改仿真文件](#修改仿真文件)
        - [修改仿真设置](#修改仿真设置)
        - [运行仿真](#运行仿真)
    - [约束](#约束)
    - [实现并烧录至设备](#实现并烧录至设备)
    - [封装](#封装)
    - [利用 1bit ALU 封装制作 4bit ALU](#利用-1bit-alu-封装制作-4bit-alu)

<!-- /TOC -->

## 环境说明

- Vivado 2015.3
- Basys3 Xilinx Artix-7 FPGA xc7a35tcpg236-1

## 新建工程

打开 Vivado，选择 Create New Project。

![new pro](http://ovi1rdu1p.bkt.clouddn.com/create-new-project.png)

此时会弹出 New Project 建立向导。输入 Project 的位置和名称， Next。

![pro name](http://ovi1rdu1p.bkt.clouddn.com/project-name.png)

选择 RTL Project， Next。随后的 Add source，Add IP，Add constraint 全部选择 Next。

在 Default part 窗口中 search xc7a35tcpg236-1，并选中之， Next。

![part](http://ovi1rdu1p.bkt.clouddn.com/default-part.png)

New Project 建立向导的最后，会弹出 Summary。核对信息，确认无误，点击 Finish。

![summ](http://ovi1rdu1p.bkt.clouddn.com/pro-summary.png)

工程新建完毕。

## 导入IP核

下载并解压全部 [74LS 系列的IP核](https://pan.baidu.com/s/1kUM5OKR#list/path=%2F%E6%95%B0%E7%94%B52017share%2Fsource_lib%2F74IP) 到一个方便的位置。

> 请不要放在 project 目录内。

在 Vivado 左侧栏选择 IP Catalog，右上部分会弹出 IP Catalog 窗口，在窗口内空白位置单击右键，选择 Add Repository。

![add IP](http://ovi1rdu1p.bkt.clouddn.com/ADD-IP.png)

![dir](http://ovi1rdu1p.bkt.clouddn.com/repos.png)

选择装有刚才解压得到的 74LS IP核的文件夹，Selete。成功后会弹出提示。此时 IP Catalog 窗口中应该会有 User Repository 一项。

![user](http://ovi1rdu1p.bkt.clouddn.com/user-reso.png)

IP核导入完毕。

## 画电路图

### 根据 ALU 功能表写出真值表

> 也可以不写，只要心里你清楚就行。

此处命名 S0 S1 S2 为控制端， A B Cn 为数据输入端， Y Cn_1 为数据输出端。

table

>这表挺简单的，先留着TBD

### 根据真值表构建电路图

在 Vivado 左侧栏选择 Create Block Design，在弹出的窗口中输入电路图的名称，点击 OK 。

> 注意，连字符 '-' 在此处是不允许的。

![block design](http://ovi1rdu1p.bkt.clouddn.com/BLOCK-DESIGN-NAME.png)

此时右上的主窗口会弹出空白的 Diagram 窗口，单击窗口中央的 Add IP 标志添加元件。你也可以随时单击右键添加元件。

右键单击元件的引脚，选择 Make External，添加输入端。

![mk ext](http://ovi1rdu1p.bkt.clouddn.com/make-ext.png)

也可以选中某一输入端，在左下方 External port porperties 窗口中改名。

![edit name](http://ovi1rdu1p.bkt.clouddn.com/ext-port-properties.png)

根据真值表画出电路图并连线。需要注意的是，Vivado 不允许元件的输入引脚悬空，所以最好充分利用所有的四联装元件，并将所有悬空的引脚连上低电平的输入端 GND。

> 需要输入高电平可以使用 GND + 非门实现。

连好之后大概是这样。电路有7个输入端，2个输出端。单击F6进行电路检查，如果出现报错，请返回电路图，自行修改。

![ALU](http://ovi1rdu1p.bkt.clouddn.com/FULL-ALU.png)

> 我刚看了一下发现连线其实是错的，你们别急着直接抄

## 仿真

### 修改仿真文件

在 Vivado 左侧栏选择 Project Manager，在 Sources 窗口中右键单击 ALU_demo.bd ，依次选择 Generate Output Products 和 Create HDL Wrapper。

> Generate Output Products 和 Create HDL Wrapper 都会弹出选项卡，使用默认设置即可。

此时， Vivado 会生成一个 `ALU_demo_wrapper.v` 文件将 ALU_demo.bd 包起来。

![wrapper](http://ovi1rdu1p.bkt.clouddn.com/wrapper.png)

依旧是在 Sources 窗口，右键单击空白处，选择 Add or create Simulation source。在弹出来的窗口中选择Add source file，并且选择 [alu_1_tb.v](https://pan.baidu.com/s/1kUM5OKR#list/path=%2F%E6%95%B0%E7%94%B52017share%2F3_Create_IPI%2Fsources&parentPath=%2F)。

> 此处提供的 Simulation source 在仿真之后得到的结果不甚直观，我会重新写一份，以免造成困惑。TBD

此时，Sources 窗口的 Simulation Sources 文件夹下会多出来一项 `alu_1_tb`。

点击 '+' 展开，会发现里面有一个带问号标志的文件。双击 `alu_1_tb` 打开，将第32行的代码

```
alu_1_wrapper uut(.A(IN1[0]),.B(IN1[1]),.Cn(IN1[2]),.Cn_1(OUT1[1]),.GND(GND),.S0(IN1[3]),.S1(IN1[4]),.S2(IN1[5]),.Y(OUT1[0]));
```

修改为

```
ALU_demo_wrapper uut(.A(IN1[0]),.B(IN1[1]),.Cn(IN1[2]),.Cn_1(OUT1[1]),.GND(GND),.S0(IN1[3]),.S1(IN1[4]),.S2(IN1[5]),.Y(OUT1[0]));
```

`ctrl+s` 保存之。

>此处修改的内容是根据 Create Block Design 时输入的文件名决定的。此内容大小写敏感。

如果修改正确的话，带问号标志的文件会消失，取而代之的是一个层级分明的文件结构。

![file](http://ovi1rdu1p.bkt.clouddn.com/file-sturc.png)

此时，仿真文件已经导入并修改完毕。

### 修改仿真设置

在 Vivado 左侧栏选择 Simulation Setting，Simulation 选项卡中的 runtime 一项改成 7000ns 以观察完整的一个仿真周期。

![simu setting](http://ovi1rdu1p.bkt.clouddn.com/simulat-setting.png)

### 运行仿真

> 从此处开始，我换用了另一个 project，因此文件名可能与上文不对应。但是

在 Vivado 左侧栏点击 Run Simulation -> Run behaviar Simulation ，开始仿真，仿真所需的时间根据电脑性能而异。

在仿真窗口左侧单击'+'以展开波形，单击 zoom fit 使波形适合屏幕。

![wave](http://ovi1rdu1p.bkt.clouddn.com/wave.png)

重新确认一遍波形是否符合真值表。

## 约束

在 Vivado 左侧栏点击 Run Synthesis，开始综合，所需的时间根据电脑性能而异。

综合结束后选择Open Synthesized Design。在左上方菜单栏中选择 windows -> I/O ports ，以打开I/O ports窗口。

![io1](http://ovi1rdu1p.bkt.clouddn.com/io-ports.png)

根据板子实体或者用户手册，选择合适的位置，并将全部 I/O std 调整为 LVCMOS33。

![io](http://ovi1rdu1p.bkt.clouddn.com/io-ports2.png)

`ctrl+s` 保存之。

## 实现并烧录至设备

在 Vivado 左侧栏点击 Run implementation，等待数分钟后，提示 implementation 成功。选择 Generate bitstream 等待数分钟后，提示 bitstream generation 成功，选择 Open hardware manager。

将实验板和电脑相连，并在点击上方提示栏，选择 auto connect，连接成功后提示栏变绿。

在左上角的 hardware 窗口，右键单击 xc7a35t_0 ，选择 program device。

bitstream file （默认）为上一步生成的 `ALU_1_wrapper.bit` ， Debug file 留空。点击program。

此时，你的板子已经可以运行所设计的逻辑了，但是还需要一步将其烧写至ROM。

选择 bitstream setting，勾选 -bin_file ，重新点击 Generate bitstream ，选择 Open hardware manager。

![](http://ovi1rdu1p.bkt.clouddn.com/bits-setting.png)

> 勾选 -bin_file,只有这样你才能得到下一步所需的 `ALU_1_wrapper.bin`

在左上角的 hardware 窗口，右键单击 xc7a35t_0 ，选择 Add configuration memory device。

> 如果之前板子有烧录内容，需要先右键删除之才可以重新烧录。

在弹出的搜索框内输入 S25FL032，选中下方第一个（也是唯一一个）芯片信号。

在弹出的program configuration memory devicd 窗口中的 configuration file 一栏中填入ALU_wrapper.bin，通常在 `ALU_1/ALU_1.runs/impl_1/ALU_1_wrapper.bin`，一路确认并且等待读条结束，提示 Flash programming 成功。

此时的板子可能是完全没有响应的状态，你需要在hardware 窗口中右键单击 xc7a35t_0 ，选择 boot from configuration device 重启之以观察效果。

## 封装

在右边栏选择 project setting 设置新生成IP核所属类别。

![ip setting](http://ovi1rdu1p.bkt.clouddn.com/self-define-IPcore.png)

在顶栏 tool 选项卡选择 Create an Package IP， next， 选择 package your current project ，next。选择IP要放置的路径，next。。


确认无误之后点击 finish，一路确认， vivado会弹出一个新的窗口。

![new tab](http://ovi1rdu1p.bkt.clouddn.com/new-tab.png)

确认名称无误， 点击 review and package，选择 re-package IP。

提示封装成功，现在可以开始制作 4bit ALU 了。

## 利用 1bit ALU 封装制作 4bit ALU

新建一个工程，导入 1bit ALU IP 核 和制作这个封装的 IP 核。

PIC

新建 block design，画电路图。

仿真部分TBD，先跳过，有空回来补

反正就是之前那一套一模一样的东西，前面学会了后面就很简单，明天就检查了，就这样吧。

