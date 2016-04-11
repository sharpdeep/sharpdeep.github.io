---
layout: post
title: Atom插件安装失败的解决办法
subtitle: ''
date: 2016-04-11T00:00:00.000Z
author: Sharpdeep
header-img: img/post-bg-2015.jpg
tags:
  - Atom
  - 问题解决
  - 记录
---

今天安装了一个Atom，想要安装几个插件的时候却死活安装不成功。Google了一下，有人说是国内npm源的问题，有人说是npm本身的问题。

对于墙引起的问题可以参考：<https://atom-china.org/t/atom/797> 的解答。

我设置了代理之后发现还是安装不成功，于是就只能选择手动安装的办法:

1. [到这里搜索需要的插件](https://atom.io/packages),然后找到插件的Github地址；
2. 进入atom的包管理目录`~/.atom/packages`，`git clone packages-repo`;
3. cd `packages-repo`,安装插件`npm install`
