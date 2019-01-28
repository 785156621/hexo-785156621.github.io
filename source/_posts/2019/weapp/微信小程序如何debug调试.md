---
title: 微信小程序如何debug调试
tags:
  - PHP
  - weapp
url: 287.html
id: 287
categories:
  - PHP
  - weapp
date: 2019-01-17 17:22:39
---

在小程序程序中调用接口地址后加：`?XDEBUG_SESSION_START=1`

即可进入debug调试模式。前提是接口地址得是本地环境。

效果：小程序调接口时会直接跳转到PhpStorm对应接口打断点处。

此方法，对`Postman`也适用。

相关链接：[https://blog.csdn.net/qq_15936309/article/details/81700650?utm_source=blogxgwz5](https://blog.csdn.net/qq_15936309/article/details/81700650?utm_source=blogxgwz5)