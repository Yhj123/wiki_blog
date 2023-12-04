---
title: ref关键字
subtitle:
date: 2023-11-18T11:22:25+08:00
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
  - 后端
categories:
  - CSharp
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

# 链接
```C++
#include <stdio.h>
#include <winsock2.h>
#pragma comment(lib, "ws2_32")

void bigOrSmall()
{
 int byte = 0x12345678;
 byte = htonl(byte);
 /*
 1位十六进制数可以用4位二进制数来表示
 16进制1位 = 2进制4位
 */
 char * ptr = (char *)&byte;
 printf("ptr  :%lu, byte  :%x \n",ptr,*ptr);
 printf("ptr+1:%lu, byte+1:%x, \n",(ptr+1),*(ptr+1));
}
int main() {
    bigOrSmall();
}
```

1. [ref 与 out 区别](https://www.cnblogs.com/gjahead/archive/2008/02/28/1084871.html)
2. [ref 与 out 区别](https://www.jianshu.com/p/3d23e20535cb)