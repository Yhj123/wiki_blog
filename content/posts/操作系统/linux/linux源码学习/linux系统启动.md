---
title: Linux系统启动
subtitle:
date: 2023-11-21T16:50:35+08:00
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
  - 操作系统
categories:
  - linux源码学习
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
## 第一行代码: 加载启动区
1. 操作系统的开发人员,会把操作系统最开始的那段代码[^1]，编译并存储在硬盘的 0 盘 0 道 1 扇区.按下开机键的那一刻，CPU会自动把代码段寄存器 CS 设置为 0xF000, 其段基地址则被设置为 0xFFFF0000, 段长度设置为 64KB。而 IP 被设置为0xFFF0,因此此时CPU代码指针指向 0xFFFFFFF0 处,即4G空间最后一个64K的最后16字节处,即系统 ROM BIOS 存放的位置.在主板上提前写死的固件程序 BIOS 会将硬盘中启动区[^2]的 512 字节的数据，原封不动复制到内存中的 0x7c00 这个位置，并跳转到那个位置进行执行.
```
mov ax,0x07c0         !将值 0x07c0 复制到 ax 寄存器里
mov ds,ax             !将 ax 寄存器里的值复制到 ds 寄存器
mov ax,0x9000
mov es,ax
mov cx,#256           ！计数器，提供需要复制的字的数量 256字=512字节
sub si,si             !sub指令作用：减法操作,即 si 寄存器清零.
sub di,di
rep                   !rep指令作用：重复执行后面一句操作，并递减cx的值，直到cx=0停止.
movw                  !movw指令作用：这里从内存 [si] 处移动 cx 个字到 [di]；注意一次的移动单位是“字”，mov指令+w（word）是一次移动一个字.
jmpi    go,INITSEG    !将BIOS移动到0x9000后，跳转（go）到INITSEG（0x9000），CS=0x90000
go:	mov	ax,cs
	mov	ds,ax
	mov	es,ax
```
{{< admonition type=abstract title="解释" open=false >}}
1. 一段 512 字节的代码和数据，从硬盘的启动区先是被移动到了内存 0x7c00 处，然后又立刻被移动到 0x90000 处，并且跳转到此处往后再稍稍偏移 go 这个标签所代表的偏移地址处，即 mov ax,cs 这行指令的位置.
{{< /admonition >}}

<iframe src="//player.bilibili.com/player.html?aid=332785594&bvid=BV1iA411V7Di&cid=331932253&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

## 参考链接
[^1]: 开始的代码是用汇编语言写的 bootsect.s(位于boot 文件夹下).
[^2]: 启动区: 硬盘中的 0 盘 0 道 1 扇区的 512 个字节的最后两个字节(0x55 和 0xaa).
[^3]: sub si,si 等同于 si = si - si.

1. [Linux内核源码学习——bootsect.s](https://www.jianshu.com/p/5454069688a2)
2. [Linux 源码趣读](https://github.com/dibingfa/flash-linux0.11-talk)
3. [linux在线源码](https://elixir.bootlin.com/linux/0.11/source)