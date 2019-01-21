---
title: php获取时间是星期几
tags:
  - PHP
url: 224.html
id: 224
categories:
  - PHP
date: 2017-09-18 16:27:06
---

PHP星期几获取代码：

date("l"); //data就可以获取英文的星期比如Sunday date("w"); //这个可以获取数字星期比如123，注意0是星期日

  获取中文星期几：

$weekarray=array("日","一","二","三","四","五","六"); //先定义一个数组 echo "星期".$weekarray\[date("w")\];

  获取指定日期是：

$weekarray=array("日","一","二","三","四","五","六"); echo "星期".$weekarray\[date("w",strtotime("2011-11-11"))\];

原文链接：http://www.cnblogs.com/jinshuo/p/6733096.html