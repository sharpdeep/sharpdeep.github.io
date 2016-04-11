---
layout: post
title: 天朝 Android Studio 更新指南
subtitle: ''
date: 2016-04-11T00:00:00.000Z
author: Sharpdeep
header-img: img/post-bg-2015.jpg
tags:
  - Android Studio
  - 科学上网
  - 记录
---

# 0x00

听说最近Google更新了2.0稳定版本的Android Studio:[Android Studio 2.0 稳定版](http://chinagdg.org/2016/04/android-studio-2-0/)，于是就想尝尝鲜更新一下。但是既然身在墙内，要更新一下Android Studio还是得有特殊的技巧。

# 0x01 为Android Studio设置代理

当然如果你直接`help`->`check for update`是不可能成功的，因为有墙。因此第一办法也是蛮简单粗暴的：**为Android Studio设置代理**：

1. 在`Settings`中找到`proxy`：设置代理：![](/img/20160411/00.png)
2. 我用的是Shadowsocks,本地端口是1080，这个可以根据自己的代理服务器修改；
3. `help`->`check for update`，发现成功连上世界：![](/img/20160411/01.png)

到了这一步，本来应该就没有问题，直接update就行了。可是在下载patch包的中途老是失败。没办法，只能用最后的绝招:**手动安装**

# 0x02 手动安装Patch包

- 首先需要确认你当前的版本有没有patch包可以升级到最新版本，在[updates.xml](https://dl.google.com/android/studio/patches/updates.xml)列出了所有的更新信息。你当前AS的版本号可以在`help`->`about`中查找(如果AS版本过老，可以选择一个中转包先)；
- 然后直接下载patch包，patch包资源的格式为

  linux: `https://dl.google.com/android/studio/patches/$from-$to-patch-unix.jar`  

  win:    `https://dl.google.com/android/studio/patches/$from-$to-patch-win.jar`

  如我是1.5.1版本，下载的地址就为:`https://dl.google.com/android/studio/patches/AI-141.2456560-143.2739321-patch-unix.jar`

- 安装patch包：

```
$android-studio：sudo java -cp ./patches/AI-141.2456560-143.2739321-patch-unix.jar com.intellij.updater.Runner install .
```

![](/img/20160411/02.png)
