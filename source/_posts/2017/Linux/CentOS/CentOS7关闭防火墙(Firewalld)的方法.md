---
title: CentOS7关闭防火墙(Firewalld)的方法
tags:
  - Linux
url: 276.html
id: 276
categories:
  - Linux
date: 2017-06-14 14:38:36
---

CentOS7开始firewalld取代了iptables，但无论是iptables还是firewalld运行都是基于系统。随着云服务的迅速发展如AWS的安全组(SecurityGroup)、阿里云的云盾提供管理简单并且功能强大的防火墙功能。因此更喜欢关闭系统的防火墙功能而使用云服务商提供的防火墙功能(阿里云的CentOS7.1默认以关闭了firewalld)。 以下是在CentOS7系统上关闭Firewalld的方法。 **查看firewalld是否开启** # systemctl is-enabled firewalld enabled **停止firewalld** # systemctl stop firewalld **确认firewalld是否停止** # systemctl status firewalld firewalld.service - firewalld - dynamic firewall daemon Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled) Active: inactive (dead) Jun 22 16:34:23 zabbix.cc systemd\[1\]: Stopped firewalld - dynamic .... Hint: Some lines were elli[ps](http://www.111cn.net/fw/photo.html)ized, use -l to show in full. **关闭firewalld的开机自动启动** # systemctl disable firewalld Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service. Removed symlink /etc/systemd/system/basic.target.wants/firewalld.service. **确认firewalld开机自动启动以关闭** # systemctl is-enabled firewalld disabled **1、firewalld简介** firewalld是centos7的一大特性，最大的好处有两个：支持动态更新，不用重启服务；第二个就是加入了防火墙的“zone”概念 firewalld有图形界面和工具界面，由于我在服务器上使用，图形界面请参照官方文档，本文以字符界面做介绍 firewalld的字符界面管理工具是 firewall-cmd firewalld默认配置文件有两个：/usr/lib/firewalld/ （系统配置，尽量不要修改）和 /etc/firewalld/ （用户配置地址） **zone概念：** 硬件防火墙默认一般有三个区，firewalld引入这一概念系统默认存在以下区域（根据文档自己理解，如果有误请指正）： drop：默认丢弃所有包 block：拒绝所有外部连接，允许内部发起的连接 public：指定外部连接可以进入 external：这个不太明白，功能上和上面相同，允许指定的外部连接 dmz：和硬件防火墙一样，受限制的公共连接可以进入 work：工作区，概念和workgoup一样，也是指定的外部连接允许 home：类似家庭组 internal：信任所有连接 对防火墙不算太熟悉，还没想明白public、external、dmz、work、home从功能上都需要自定义允许连接，具体使用上的区别还需高人指点