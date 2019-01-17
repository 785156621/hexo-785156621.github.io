---
title: navicat EDB xDB need pg_authid.rolcatupdate ?
tags:
  - SQL
url: 286.html
id: 286
categories:
  - SQL
date: 2017-05-04 13:49:36
---

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504134616.png)

PostgreSQL 9.5以前的版本，pg_authid有个字段rolcatupdate，用来标记用户是否有更新catalog的权限。 如果rolcatupdate=false，即使是超级用户也不能更新catalog。

解决方法：更新一下navicat版本吧 ![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504134815.png) 相关链接：[https://yq.aliyun.com/articles/27080#](https://yq.aliyun.com/articles/27080#) [https://www.navicat.com.cn/download/navicat-for-postgresql](https://www.navicat.com.cn/download/navicat-for-postgresql)