---
title: 不可不知的centos7 firewalld 防火墙的使用
tags:
  - Linux
url: 277.html
id: 277
categories:
  - Linux
date: 2017-06-14 14:39:53
---

centos7 firewalld 防火墙的使用

FirewallD is not running
========================

是你的防火墙还没开。 可以执行 systemctl start firewalld 开启防火墙。

相关命令 CentOS 7 上systemctl 的用法
----------------------------

[http://www.linuxidc.com/Linux/2014-11/109236.htm](http://www.linuxidc.com/Linux/2014-11/109236.htm)

### systemctl status firewalld

![](http://huanggd.com/wp-content/uploads/2017/06/1380519315-5633220f2fcc4_articlex.png)

firewalld使用简介
=============

[http://www.centoscn.com/CentOS/help/2015/0208/4667.html](http://www.centoscn.com/CentOS/help/2015/0208/4667.html)

Centos7 开放端口
============

Centos升级到7之后，发现无法使用iptables控制Linuxs的端口，google之后发现Centos 7使用firewalld代替了原来的iptables。下面记录如何使用firewalld开放Linux端口： 开启端口 firewall-cmd --zone=public --add-port=80/tcp --permanent 命令含义： --zone #作用域 --add-port=80/tcp #添加端口，格式为：端口/通讯协议 --permanent #永久生效，没有此参数重启后失效 重启防火墙 firewall-cmd --reload 详细信息可以参考以下资料： [http://stackoverflow.com/questions/24729024/centos-7-open-firewall-port](http://stackoverflow.com/questions/24729024/centos-7-open-firewall-port) [https://access.redhat.com/documentation/en-US/Red\_Hat\_Enterprise\_Linux/7/html/Security\_Guide/sec-Using_Firewalls.html](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Security_Guide/sec-Using_Firewalls.html) 相关链接：https://segmentfault.com/a/1190000003931716 http://www.cnblogs.com/yangxunwu1992/p/6091422.html