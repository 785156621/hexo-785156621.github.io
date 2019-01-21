---
title: 局域网内访问Homestead环境
tags:
  - Laravel
url: 272.html
id: 272
categories:
  - Laravel
  - PHP
date: 2017-12-13 14:00:40
---

最近在使用laravel开发app接口，本地机器安装了Homestead，app想通过局域网访问我这台程序接口，那如何设置可以让局域网访问呢？ 1.查看局域网ip地址 ![](http://gdmizi.com/wp-content/uploads/2017/12/QQ截图20171213135705.png) 可以看到我机器ip 192.168.0.18 2.找到Homestead里的Homestead.yaml添加如下配置 networks: - type: "public_network" ip: "192.168.0.25"         //这里是重点，配置成局域网同ip段的 bridge: "en1: Wi-Fi (AirPort)" 参考官方网站文档说明如下： ![](http://gdmizi.com/wp-content/uploads/2017/12/QQ截图20171213135902.png) 3.重启vagrant `vagrant reload`   相关链接：http://www.bcty365.com/content-153-5910-1.html