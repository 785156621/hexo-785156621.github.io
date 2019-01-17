---
title: windows（64位）下使用curl命令
tags:
  - PHP
url: 243.html
id: 243
categories:
  - PHP
date: 2017-11-29 15:35:48
---

> Curl命令可以通过命令行的方式，执行Http请求。在Elasticsearch中有使用的场景，因此这里研究下如何在windows下执行curl命令。

工具下载
----

在官网处下载工具包：[http://curl.haxx.se/download.html](http://curl.haxx.se/download.html) ![](http://images0.cnblogs.com/blog2015/449064/201507/162140236889309.png)  

使用方式一：在curl.exe目录中使用
--------------------

解压下载后的压缩文件，通过cmd命令进入到curl.exe所在的目录。 由于博主使用的是windows 64位 的系统，因此可以使用I386下的curl.exe工具。 进入到该目录后，执行curl --help测试： ![](http://images0.cnblogs.com/blog2015/449064/201507/162145094232084.png)

使用方式二：放置在system32中
------------------

解压下载好的文件，拷贝I386/curl.exe文件到C:\\Windows\\System32 然后就可以在DOS窗口中任意位置，使用curl命令了。

使用方式三：配置环境变量
------------

在系统高级环境变量中，配置 CURL\_HOME ----- "你的curl目录位置\\curl-7.43.0" path ---- 末尾添加 “;%CURL\_HOME%\\I386” 这样与上面方式二的效果相同。   原文链接：https://www.cnblogs.com/xing901022/p/4652624.html