---
title: Docker中配置国内镜像
tags:
  - Docker
url: 247.html
id: 247
categories:
  - Docker
date: 2017-12-08 14:43:24
---

**1\. 为什么要为docker配置国内镜像**
-------------------------

在正常情况下，docker有一个默认连接的国外官方镜像，在国外的网友访问该官方镜像自然不成问题，但是国内毕竟不是国外，由于国情不同，中国的网络访问国外官方镜像网速一向很慢，而且往往还会遭遇断网的窘境，所以说我们要想正常使用docker的镜像，那么我们就不得不配置相应的国内镜像。

**2\. 可以使用的国内镜像有哪些**
--------------------

Docker可以配置的国内镜像有很多可供选择，比如说：阿里云，网易蜂巢，DaoCloud，Docker中国区官方镜像等，这些都是可以提供给大家随意选择的不错的镜像仓库。

**3\. 配置Docker中国区官方镜像**
-----------------------

### **1\. Docker中国区官方镜像简介**

在国内，可以通过registry.docker-cn.com访问官方镜像库，目前该镜像库只包含流行的公有镜像，而私有镜像仍需要从美国镜像库中拉取。

### **2\. 配置Docker中国区官方镜像**

使用vi修改 /etc/docker/daemon.json 文件并添加上”registry-mirrors”: \[“[https://registry.docker-cn.com](https://registry.docker-cn.com/)“\]，如下：

> vi /etc/docker/daemon.json { “registry-mirrors”: \[“[https://registry.docker-cn.com](https://registry.docker-cn.com/)“\] }

### **3\. 重启Docker**

配置完之后执行下面的命令，以使docker的配置文件生效

> systemctl daemon-reload systemctl restart docker

**4\. 测试配置的结果**
---------------

### **1\. busybox简介**

我们可以通过从镜像仓库中拉去镜像的方式来测试镜像地址是否配置成功，比如说我们可以尝试去拉取一个简单的busybox镜像来进行相应的测试。 busybox是一个集成了一百多个最常用linux命令和工具的软件,同时它也是一个最小的Linux系统，它提供了该系统的主要功能，例如grep、find、mount以及telnet等但不包含一些与GNU相关的功能和选项。

### **2\. 拉取busybox**

执行指令如下：

> docker pull busybox

当看到下面的信息时，说明镜像已经拉取成功

> Using default tag: latest Trying to pull repository docker.io/library/busybox … latest: Pulling from docker.io/library/busybox 9e87eff13613: Pull complete Digest: sha256:2605a2c4875ce5eb27a9f7403263190cd1af31e48a2044d400320548356251c4

### **3\. 测试busybox**

测试拉取的busybox镜像

> \[root@localhost ~\]# docker run busybox echo “hello world” hello world

当我们看到控制台打印出的“hello world”时，这就说明我们的busybox已经测试成功了。   原文链接：http://blog.csdn.net/zzy1078689276/article/details/77371782