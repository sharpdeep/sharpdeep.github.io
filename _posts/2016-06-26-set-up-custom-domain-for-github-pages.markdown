---
layout: post
title: 为你的Github Pages博客绑定一个免费顶级域名吧
subtitle: ''
date: 2016-06-26T00:00:00.000Z
author: Sharpdeep
header-img: img/post-bg-2015.jpg
tags:
  - Github Pages
  - 域名
  - DNSPod
  - DNS
---

# 1. 申请一个免费顶级域名

免费顶级域名我们可以去[Freenom](https://my.freenom.com/clientarea.php)申请，最长可以申请一年的免费域名使用权，至于一年后续期是否是免费的，我在官网没有看到相关说明。

Freenom提供的顶级域名包括

- tk
- ml
- ga
- cf
- gq

并没有我们常见的com，cn和net这些域名，当然如果不差钱的话，也可以去申请万网申请一个付费域名。

申请流程非常简单：

- 注册用户
- [查询并选择一个域名](https://my.freenom.com/domains.php)

![](/img/20160626/00.png)

- checkout,continue,填写相关用户信息，提交订单

![](/img/20160626/01.png)

现在你已经拥有自己的顶级域名了，可以在[MyDomains](https://my.freenom.com/clientarea.php?action=domains)查看

# 2. 添加CNAME文件

在你的github pages项目根目录上新建一个CNAME文件，在CNAME文件上编辑刚才申请到的域名，比如，刚才申请到`itcoding.tk`，那么我就写上`itcoding.tk`(推荐)，当然你也可以写`www.itcoding.tk`，两种写法处理方式不同：

- 如果你写的是`itcoding.tk`，那么`www.itcoding.tk`就会指向`itcoding.tk`
- 如果你写的是`www.itcoding.tk`,那么`itcoding.tk`就会指向`www.itcoding.tk`

注意，两种写法都不需要在前面加`http`。

这个CNAME文件有什么用呢？稍后再说。

# 3. 在DNSPod添加A记录

这里涉及到DNS的一些知识，如果你想了解DNS，可以先看一下[DNS原理入门](http://www.ruanyifeng.com/blog/2016/06/dns.html)。知道什么是A记录，什么是CNAME记录也就行了。

- 首先[注册DNSPod账号](https://www.dnspod.cn)，然后进入管理中心，选择添加域名。

![](/img/20160626/02.png)

- 为域名添加记录，这里的NS记录是自动生成，不用修改，因为我们需要我们的网站可以通过`itcoding.tk`和`www.itcoding.tk`都能访问，所以需要添加两组A记录。

![](/img/20160626/03.png)

为什么`192.30.252.153`和`192.30.252.154`，因为这是github pages官网说的咯。网上有些人说A记录是`ping xxx.github.io`之后的IP地址，这些都是不可信的。

但是你可能会奇怪，每个人都是这两个IP地址的话，那么Github怎么知道我的域名`itcoding.tk`和`www.itcoding.tk`对应的是`sharpdeep.github.io`而不是其他人的github pages呢？答案就在上一步操作中的CNAME文件，这里指定了其所对应的域名，github会自动处理，将两者对应起来。

另外，如果你添加CNAME记录把域名指向`xxx.github.io`的话，也会成功(网上某些教程就是这么做的)。但是官方是不推荐最终做法的，因为可能会"导致其他服务出现问题"。

# 4. 修改域名DNS地址

因为我们是在Freenom注册的域名，那么域名默认的DNS是Freenom提供，因为我们使用DNSPod，所以就需要到Freenom修改DNS地址，把域名解析交给DNSPod。

- 进入[MyDomains](https://my.freenom.com/clientarea.php?action=domains) -> Manage Domain -> Management Tools -> NameServers。然后把DNSPod中的两个NS记录写入。

![](/img/20160626/04.png)

- 点击保存，然后等待全球递归DNS服务器刷新（最多72小时）

配置生效后，我们就可以通过`itcoding.tk`或`www.itcoding.tk`访问博客了。

![](/img/20160626/05.png)

本文是根据Github Pages官方帮助文档写的，如果你想看官方文档，请移步：[About supported custom domains](https://help.github.com/articles/about-supported-custom-domains/)
