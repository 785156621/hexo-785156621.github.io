---
title: Windows环境下Composer的安装教程
tags:
  - PHP
url: 284.html
id: 284
categories:
  - PHP
date: 2017-05-12 17:02:24
---

1.先下载Composer-Setup.exe，下载地址：[下载Composer](https://getcomposer.org/Composer-Setup.exe) 。会自动搜索[PHP](http://lib.csdn.net/base/php "PHP知识库").exe的安装路径,如果没有，就手动找到php路径下的php.exe。 2.在PHP目录下，打开php.ini文件，开启openssl扩展。去掉extension=php\_openssl.dll前面的分号(;) 3.把php目录添加到环境变量（和php.exe同级目录的路径）例如：D:\\apache\_php\\php添加到环境变量path里。 4.下载composer.phar,下载地址：[Composer.phar](https://getcomposer.org/composer.phar) 。将composer.phar文件放入php目录下，在php目录下新建一个文件composer.cmd，内容写成：@php "%~dp0composer.phar" %*保存。运行这个文件，然后打开cmd运行：composer会出现 ![](http://img.blog.csdn.net/20160827092737772?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center) 可以运行**composer --version** 查看composer的版本。 5.在命令行中执行：`**composer config -g repo.packagist composer https://packagist.phpcomposer.com**` `改写Packagist 镜像至国内镜像可以加快下载速度。` 最后提一下，看云上有composer的中文手册[**http://www.kancloud.cn/thinkphp/composer**](http://www.kancloud.cn/thinkphp/composer)

转：http://blog.csdn.net/iloveyougirls/article/details/52333597