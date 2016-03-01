---
layout:     post
title:      "Welcome to Sharpdeep Blog"
subtitle:   " \"Hello World, Hello Blog\""
date:       2016-03-01
author:     "Sharpdeep"
header-img: "img/post-bg-2015.jpg"
tags:
    - 生活
    - 记录
---

Welcome！

第一篇Blog就来写写捣鼓这个Blog的过程，以及中间遇到的坑吧！


## Jekyll + Github Pages搭建个人Blog

Jekyll是Ruby下的一个Blog生成工具，而之前没有接触过Ruby，因此在搭建过程中基本是边摸索边做，也因此遇到了不少的坑。谨以此文记下搭建过程以及遇到的坑。


## 为什么会想要搭建一个个人网站

有这个想法是因为看到了阮一峰的这篇博文：[《搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门》](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)，查了一下，发现Jekyll + Github Pages搭建一个静态博客好像很“简单”(后来发现还是有坑)，因此就打算自己也动手搭一个。


## 安装Ruby

因为Jekyll是Ruby实现的，所以不得不接触他呀。我找到了几种安装Ruby的方法(我是在Ubuntu下)，列举如下：

 - apt-get安装

```
# sudo apt-get update
# sudo apt-get install ruby2.3 ruby2.3-dev
```

---

 - ppa安装

```
# sudo apt-get install python-software-properties
# sudo apt-add-repository ppa:brightbox/ruby-ng
# sudo apt-get update
# sudo apt-get install ruby2.3 ruby2.3-dev
```

---

 - RVM安装

RVM是ruby的版本管理工具，有了这个可以安装多个版本的ruby
首先安装RVM

```
# gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
# sudo curl -L get.rvm.io | bash -s stable
```

**此处有坑**  
rvm安装在`$HOME/.rvm`下，而安装脚本只是将`$HOME/.rvm/bin`终端加载脚本(我是.zshrc)中，我们需要手动再加一句：

```
[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # This loads RVM into a shell session.  
```

安装RVM环境依赖：

```
rvm requirements
```

安装RUby

```
rvm list known #列出已知的所有版本
rvm install ruby-2.2 --head
```

**此处又有坑**  
安装ruby的时候很可能会出现一个openssl相关的错误，查了很多资料都没能解决，讨论较多的是[这个帖子](https://ruby-china.org/topics/8589#reply24)，但是任然没有一个能解决。然后尝试安装2.3版本时：

```
rvm install 2.3.0
```
竟然成功了？！一看，原来是找到了二进制文件，不用编译了。 = =


---

## 关于gem的一个坑

安装好ruby后，gem也一起装好了，gem是一个包管理器，相当于python中的pip。但是这里也有一个坑：gem的源在国外，由于众所周知的原因，经常出现连接问题或者速度太慢，好在淘宝做了一个镜像，可以：

```
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
```



## 安装一些包

安装jekyll

```
gem install jekyll
```



## 下载Jekyll模板

我这里选用了[HuxPro](https://link.zhihu.com/?target=https%3A//github.com/Huxpro/huxpro.github.io)
按照其引导，下载模板到本地：

```
 git clone git@github.com:Huxpro/huxblog-boilerplate.git
```

并改名为`sharpdeep.github.io`(自己修改)
然后按照[这个](https://github.com/Huxpro/huxpro.github.io/blob/master/README.zh.md#environment)中的进行。
