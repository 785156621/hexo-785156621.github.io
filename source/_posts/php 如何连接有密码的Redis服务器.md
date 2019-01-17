---
title: php 如何连接有密码的Redis服务器
tags:
  - Redis
url: 202.html
id: 202
categories:
  - Redis
date: 2017-09-05 16:56:32
---

      //实例化  
      $redis = new Redis();  
      //连接服务器  
      $redis->connect("localhost");  
      //授权  
      $redis->auth("passwd");  
      //相关操作  
      $redis->set("name","father");  
      $data = $redis->key("*");  
      var_dump($data);  

相关链接：[https://segmentfault.com/q/1010000005005907](https://segmentfault.com/q/1010000005005907)