---
title: win10 专业版安装docker
tags:
  - Docker
url: 245.html
id: 245
categories:
  - Docker
date: 2017-12-05 11:00:01
---

1\. 前言
======

Docker最近推出了可以运行在Win10和Mac上的稳定版本，让我们赶紧来体验一下。  

2\. 安装准备
========

需要的条件为： 64bit Windows 10，开启Hyper-V 注意：win10家庭版无法开启Hyper-V，可以升级为专业版  

### 2.1 下载Docker for Windows

从官网的下面地址可以下载 https://download.docker.com/win/stable/InstallDocker.msi  

### 2.2 开启win10的Hyper-V

控制面板 -> 程序 -\> 启用或关闭Windows功能 -> 选中Hyper-V ![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801102305137-1724102174.png) 完成后自动重启  

3\. 安装Docker
============

用刚才下载的安装包安装，安装完成后，启动Docker 如果没有开启Hyper-V，启动Docker的时候会提示开启Hyper-V ![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801102654903-565448835.png)   如果启动的时候，提示内存不足，启动失败，可以在设定中调节VM内存大小 ![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801102950856-209620072.png)  

4\. 使用Docker
============

### 4.1 查看版本等信息

docker info

![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801103202747-665891052.png)  

### 4.2 run hello world

docker run hello-world

![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801103324872-1203371760.png)  

### 4.3 启动一个Ubuntu容器

docker run -it ubuntu bash

![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801110626981-801038178.png)  

### 4.4 查看所有容器

docker ps -a

![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801110938231-76561349.png)  

### 4.5 启动一个nginx容器

docker run -d -p 81:80 --name webserver nginx

![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801113038715-954002212.png)   查看运行中的容器

docker ps

![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801113123028-1841727172.png)   浏览器访问确认 ![](https://images2015.cnblogs.com/blog/868522/201608/868522-20160801113225372-1434728896.png)  

5\. 后记
======

Docker终于有了可以运行在Win10和Mac上的稳定版本，可以尝试在生产环境部署一下。   原文链接：https://www.cnblogs.com/ee900222/p/docker_4.html 相关链接：https://jingyan.baidu.com/article/642c9d340202e2644a46f796.html