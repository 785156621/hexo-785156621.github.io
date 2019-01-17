---
title: systemctl管理Redis启动、停止、开机启动
tags:
  - Redis
url: 199.html
id: 199
categories:
  - Redis
date: 2017-09-05 12:23:32
---

1\. 创建服务
========

用service来管理服务的时候，是在`/etc/init.d/`目录中创建一个脚本文件，来管理服务的启动和停止，在systemctl中，也类似，文件目录有所不同，在`/lib/systemd/system`目录下创建一个脚本文件redis.service，里面的内容如下：

    [Unit]
    Description=Redis
    After=network.target
    
    [Service]
    ExecStart=/usr/local/bin/redis-server /usr/local/redis/redis.conf  --daemonize no
    ExecStop=/usr/local/bin/redis-cli -h 127.0.0.1 -p 6379 shutdown
    
    [Install]
    WantedBy=multi-user.target
    

> 更详细的service文件说明请访问：[这里](http://www.csdn.net/article/2015-02-27/2824034)

2\. 创建软链接
---------

创建软链接是为了下一步系统初始化时自动启动服务

    ln -s /lib/systemd/system/redis.service /etc/systemd/system/multi-user.target.wants/redis.service

> 创建软链接就好比Windows下的快捷方式 ln -s 是创建软链接 ln -s 原文件 目标文件（快捷方式的决定地址）

如果创建软连接的时候出现异常，不要担心，看看`/etc/systemd/system/multi-user.target.wants/` 目录是否正常创建软链接为准，有时候报错只是提示一下，其实成功了。

    $ ll /etc/systemd/system/multi-user.target.wants/
    total 8
    drwxr-xr-x  2 root root 4096 Mar 30 15:46 ./
    drwxr-xr-x 13 root root 4096 Mar 13 14:18 ../
    lrwxrwxrwx  1 root root   31 Nov 23 14:43 redis.service -> /lib/systemd/system/redis.service
    ...略...

3\. 刷新配置
--------

刚刚配置的服务需要让systemctl能识别，就必须刷新配置

    $ systemctl daemon-reload

如果没有权限可以使用sudo

    $ sudo systemctl daemon-reload

* * *

4\. 启动、重启、停止
------------

启动redis

    $ systemctl start redis

重启redis

    $ systemctl restart redis

停止redis

    $ systemctl stop redis

5\. 开机自启动
---------

redis服务加入开机启动

    $ systemctl enable redis

禁止开机启动

    $ systemctl disable redis

6\. 查看状态
--------

查看状态

    $ systemctl status redis
    
    
    原文链接：http://blog.csdn.net/chwshuang/article/details/68489968