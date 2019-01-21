---
title: xampp配置xdebug
tags:
  - PHP
  - Xampp
url: 162.html
id: 162
categories:
  - PHP
date: 2017-08-21 21:08:01
---

1.Xdebug是一个开放源代码的PHP程序调试器(即一个Debug工具)，可以用来跟踪，调试和分析PHP程序的运行状况。Xdebug现在的最新版本是Xdebug 2.4.0RC4,release日期 2016-01-25，添加了对PHP7的支持。 官方网站：[https://xdebug.org/](https://xdebug.org/) 2.下载 ![](http://gdmizi.com/wp-content/uploads/2017/08/QQ截图20170823110514-1024x181.png) 3\. 找到和自己PHP版本对应的xdebug版本，我的是最后一个 ![](http://gdmizi.com/wp-content/uploads/2017/08/QQ截图20170823110624.png) 4.把下载的xdebug放在ext文件夹下 ![](http://gdmizi.com/wp-content/uploads/2017/08/QQ截图20170823110751.png) 5.打开[php](http://lib.csdn.net/base/php "PHP知识库").ini，在最后加入下列代码 ![](http://gdmizi.com/wp-content/uploads/2017/08/QQ截图20170823110957.png) 6.检查Xdebug是否安装成功，查看phpinfo ![](http://gdmizi.com/wp-content/uploads/2017/08/QQ截图20170823111113-1024x838.png)   相关链接：[http://blog.csdn.net/wheat_ground/article/details/51982118](http://blog.csdn.net/wheat_ground/article/details/51982118)