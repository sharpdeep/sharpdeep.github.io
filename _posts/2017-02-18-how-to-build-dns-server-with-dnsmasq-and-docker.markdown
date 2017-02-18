---
layout: post
title: docker + dnsmasq 搭建DNS服务器
subtitle: ''
date: 2017-02-18T00:00:00.000Z
author: Sharpdeep
header-img: img/post-bg-2015.jpg
tags:
  - docker  
  - dnsmasq
  - DNS
---

# 1.准备环境

- 安装好docker，最好把加速器也弄好了
- 拉取dnsmasq镜像

```
docker pull andyshinn/docker:2.75
```

# 2.运行dnsmasq

```
docker run -d -p 53:53/tcp -p 53:53/udp --cap-add=NET_ADMIN --name dns_server andyshinn/dnsmasq
```

这一步很可能会出现端口被占用的情况，先查出是哪个进程在使用53端口(`netstat -anp | grep 53`)，然后kill

运行成功后查看容器是否已经在运行了

```
docker ps
```

# 3.配置dnsmasq

进入容器

```
docker exec -it dns_server /bin/sh
```

编辑`dnsmasq.conf`

```
address=/test.com/1.2.3.4
```

test.com域名就会解析到1.2.3.4了

重启一下容器

```
docker restart dns_server
```

# 4.添加多个dns服务器

我们可以用docker同时运行多个容器，但是从外部来看只有一个IP，为了让每个docker容器都能有一个独立的外部IP，我们需要更改一下运行方式


假设，设备有两个IP，192.168.1.100和192.168.1.101

```
docker run -d -p 192.168.1.100:53:53/tcp -p 192.168.1.100:53:53/udp --cap-add=NET_ADMIN --name dns_server andyshinn/dnsmasq
```

```
docker run -d -p 192.168.1.101:53:53/tcp -p 192.168.1.101:53:53/udp --cap-add=NET_ADMIN --name dns_server2 andyshinn/dnsmasq
```

`docker ps`可以看到有两个容器在运行
