---
title: STM32工程结构以及开发流程
subtitle:
date: 2023-12-04T15:43:23+08:00
draft: false
author:
  name:
  link:
  email:
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - STM32
categories:
  - 嵌入式
hiddenFromHomePage: false
hiddenFromSearch: false
summary:
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---

<!--more-->
## 文件结构

### STM32F10x_StdPeriph_Lib_V3.6.0 文件树

```txt
STM32F10x_StdPeriph_Lib_V3.6
 ├── Libraries                        // 驱动库的源代码与启动文件
 ├── Project                          // 驱动库写的例子和一个工程模版
 ├── stm32f10x_stdperiph_lib_um.chm   // 固件库使用手册和应用举例
 └── Utilities                        // ST 公司评估板的相关例程代码
```

#### Libraries 文件夹
```txt
Libraries
 ├── CMSIS                          // Cortex-M3 内核自带的外设驱动代码和启动代码
 │   ├── CM3
 │   │   ├── CoreSupport            // Cortex-M3 内核自带的外设驱动代码
 │   │   │   ├── core_cm3.c
 │   │   │   └── core_cm3.h
 │   │   └── DeviceSupport
 │   │       └── ST
 │   │           └── STM32F10x
 │   │               ├── LICENSE.txt
 │   │               ├── Release_Notes.html
 │   │               ├── startup    // 包含 arm 等四个对应不同开发环境的启动代码文件夹
 │   │               │   ├── arm    // 对应 Keil 开发环境下不同容量(小(LD),中(MD),大(HD)容量Flash)芯片的启动代码.
 │   │               │   │   ├── startup_stm32f10x_cl.s
 │   │               │   │   ├── startup_stm32f10x_hd.s
 │   │               │   │   ├── startup_stm32f10x_hd_vl.s
 │   │               │   │   ├── startup_stm32f10x_ld.s
 │   │               │   │   ├── startup_stm32f10x_ld_vl.s
 │   │               │   │   ├── startup_stm32f10x_md.s
 │   │               │   │   ├── startup_stm32f10x_md_vl.s
 │   │               │   │   └── startup_stm32f10x_xl.s
 │   │               │   ├── gcc_ride7
 │   │               │   │   ├── startup_stm32f10x_cl.s
 │   │               │   │   ├── startup_stm32f10x_hd.s
 │   │               │   │   ├── startup_stm32f10x_hd_vl.s
 │   │               │   │   ├── startup_stm32f10x_ld.s
 │   │               │   │   ├── startup_stm32f10x_ld_vl.s
 │   │               │   │   ├── startup_stm32f10x_md.s
 │   │               │   │   ├── startup_stm32f10x_md_vl.s
 │   │               │   │   └── startup_stm32f10x_xl.s
 │   │               │   ├── iar
 │   │               │   │   ├── startup_stm32f10x_cl.s
 │   │               │   │   ├── startup_stm32f10x_hd.s
 │   │               │   │   ├── startup_stm32f10x_hd_vl.s
 │   │               │   │   ├── startup_stm32f10x_ld.s
 │   │               │   │   ├── startup_stm32f10x_ld_vl.s
 │   │               │   │   ├── startup_stm32f10x_md.s
 │   │               │   │   ├── startup_stm32f10x_md_vl.s
 │   │               │   │   └── startup_stm32f10x_xl.s
 │   │               │   └── TrueSTUDIO
 │   │               │       ├── startup_stm32f10x_cl.s
 │   │               │       ├── startup_stm32f10x_hd.s
 │   │               │       ├── startup_stm32f10x_hd_vl.s
 │   │               │       ├── startup_stm32f10x_ld.s
 │   │               │       ├── startup_stm32f10x_ld_vl.s
 │   │               │       ├── startup_stm32f10x_md.s
 │   │               │       ├── startup_stm32f10x_md_vl.s
 │   │               │       └── startup_stm32f10x_xl.s
 │   │               ├── stm32f10x.h
 │   │               ├── system_stm32f10x.c
 │   │               └── system_stm32f10x.h
 │   ├── CMSIS changes.htm
 │   ├── CMSIS debug support.htm
 │   ├── Documentation
 │   │   └── CMSIS_Core.htm
 │   └── License.doc
 └── STM32F10x_StdPeriph_Driver     // Cortex-M3 内核上外加的外设驱动代码
     ├── inc                        // include缩写
     │   ├── misc.h
     │   ├── stm32f10x_adc.h
     │   ├── stm32f10x_bkp.h
     │   ├── stm32f10x_can.h
     │   ├── stm32f10x_cec.h
     │   ├── stm32f10x_crc.h
     │   ├── stm32f10x_dac.h
     │   ├── stm32f10x_dbgmcu.h
     │   ├── stm32f10x_dma.h
     │   ├── stm32f10x_exti.h
     │   ├── stm32f10x_flash.h
     │   ├── stm32f10x_fsmc.h
     │   ├── stm32f10x_gpio.h
     │   ├── stm32f10x_i2c.h
     │   ├── stm32f10x_iwdg.h
     │   ├── stm32f10x_pwr.h
     │   ├── stm32f10x_rcc.h
     │   ├── stm32f10x_rtc.h
     │   ├── stm32f10x_sdio.h
     │   ├── stm32f10x_spi.h
     │   ├── stm32f10x_tim.h
     │   ├── stm32f10x_usart.h
     │   └── stm32f10x_wwdg.h
     ├── LICENSE.txt
     ├── Release_Notes.html
     └── src                        // source 缩写
         ├── misc.c
         ├── stm32f10x_adc.c
         ├── stm32f10x_bkp.c
         ├── stm32f10x_can.c
         ├── stm32f10x_cec.c
         ├── stm32f10x_crc.c
         ├── stm32f10x_dac.c
         ├── stm32f10x_dbgmcu.c
         ├── stm32f10x_dma.c
         ├── stm32f10x_exti.c
         ├── stm32f10x_flash.c
         ├── stm32f10x_fsmc.c
         ├── stm32f10x_gpio.c
         ├── stm32f10x_i2c.c
         ├── stm32f10x_iwdg.c
         ├── stm32f10x_pwr.c
         ├── stm32f10x_rcc.c
         ├── stm32f10x_rtc.c
         ├── stm32f10x_sdio.c
         ├── stm32f10x_spi.c
         ├── stm32f10x_tim.c
         ├── stm32f10x_usart.c
         └── stm32f10x_wwdg.c
```

####  Project文件夹

```text
Project
 ├── STM32F10x_StdPeriph_Examples
 └── STM32F10x_StdPeriph_Template
```

##### STM32F10x_StdPeriph_Template 文件夹
```text
STM32F10x_StdPeriph_Template
 ├── EWARM
 ├── HiTOP
 ├── LICENSE.txt
 ├── main.c
 ├── MDK-ARM
 ├── Release_Notes.html
 ├── RIDE
 ├── stm32f10x_conf.h       // 外设头文件配置文件  
 ├── stm32f10x_it.c         // 中断函数文件
 ├── stm32f10x_it.h
 ├── system_stm32f10x.c     // 更改程序的时钟配置,根据 HSE 或者 HSI 设置系统时钟和总线时钟(AHB, APBI, APB2总线).
 └── TrueSTUDIO
```

### startup_stm32xxxxx.s 文件
- startup_stm32xxxxx.s的文件中使用汇编语言写好了基本程序，当STM32芯片上电启动的时候，首先会执行这里的汇编程序，从而建立C语言的运行环境，所以这个文件称为**启动文件**.
- startup_stm32xxxxx.s 文件功能:
  - 初始化堆栈指针SP.
  - 初始化程序计数器指针PC.
  - 设置堆和栈的大小.
  - 设置中断向量表的入口地址.
  - 配置外部SRAM作为数据存储器(由用户配置, 一般的开发板没有外部SRAM).
  - 调用SystemInit()函数配置 STM32 的系统时钟.
  - 设置C库的分支入口“__main”(最终用来调用main函数).

###  stm32f4xx.h 文件
- 根据 STM32 的存储分配先定义好各个寄存器的地址,把这些地址定义都统一写在 stm32f4xx.h 文件中.

### main.c 文件

