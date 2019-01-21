---
title: CentOS 7 安装、配置、使用 PostgreSQL 9.5安装及基础配置
tags:
  - PostgreSQL
  - SQL
url: 289.html
id: 289
categories:
  - PostgreSql
  - SQL
date: 2017-05-03 17:10:16
---

> 一直不知道怎么读这个数据库的名字，在官网上找到了文档。 PostgreSQL is pronounced Post-Gres-Q-L. [读音](http://www.postgresql.org/files/postgresql.mp3) [What is PostgreSQL? How is it pronounced? What is Postgres?](http://wiki.postgresql.org/wiki/FAQ#What_is_PostgreSQL.3F_How_is_it_pronounced.3F_What_is_Postgres.3F)

近期由于项目需要，准备使用PostgreSQL数据库，查阅了一些数据库，决定使用PostgreSQL 9.5，网上找了一些资料，实践后，将过程写下来，以备之后再使用时查看。 由于项目操作系统一直使用CentOS 7，所以搭配使用CentOS7+PostgreSQL9.5 。

> 操作系统版本：Linux localhost.localdomain 3.10.0-327.18.2.el7.x86\_64 #1 SMP Thu May 12 11:03:55 UTC 2016 x86\_64 x86\_64 x86\_64 GNU/Linux 数据库版本： psql (PostgreSQL) 9.5.3

安装过程参考官方文档，地址列于此，[Linux downloads (Red Hat family)](https://www.postgresql.org/download/linux/redhat/) 。 CentOS Yum 工具安装，简单方便，查看了一下官方源版本，显示目前最新版本是9.2.15,需要更新源，文档中有专门的rpm包列表，[RPM LIST](http://yum.postgresql.org/repopackages.php)。

> 1.添加RPM yum install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-x86_64/pgdg-centos95-9.5-2.noarch.rpm 2.安装PostgreSQL 9.5 yum install postgresql95-server postgresql95-contrib 3.初始化数据库 /usr/pgsql-9.5/bin/postgresql95-setup initdb             如无法使用可以换为service postgresql-9.5 initdb
> 
> ![](http://upload-images.jianshu.io/upload_images/2167535-e57b338fc4b2ec22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> 
> 4.设置开机自启动 systemctl enable postgresql-9.5.service 5.启动服务 systemctl start postgresql-9.5.service
> 
> ![](http://upload-images.jianshu.io/upload_images/2167535-b2fde93d27e8c9b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

自此，PostgreSQL 9.5 安装完成，此过程中注意安装权限，我在安装过程中一直使用的是root用户进行的安装。 接下来，进行一下简单的配置。 PostgreSQL 安装完成后，会建立一下‘postgres’用户，用于执行PostgreSQL，数据库中也会建立一个'postgres'用户，默认密码为自动生成，需要在系统中改一下。

> 6.修改用户密码 su - postgres  切换用户，执行后提示符会变为 '-bash-4.2$' psql -U postgres 登录数据库，执行后提示符变为 'postgres=#' ALTER USER postgres WITH PASSWORD 'abc123'  设置postgres用户密码 \\q  退出数据库
> 
> ![](http://upload-images.jianshu.io/upload_images/2167535-e6447a33d4885fee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

系统管理用的帐号和密码变更完成，现在配置一下远程连接。

> 7.开启远程访问 vi /var/lib/pgsql/9.5/data/postgresql.conf 修改#listen\_addresses = 'localhost'  为  listen\_addresses='*' 当然，此处‘*’也可以改为任何你想开放的服务器IP
> 
> ![](http://upload-images.jianshu.io/upload_images/2167535-6493b2b5d28a1ed9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> 
> 8.信任远程连接 vi /var/lib/pgsql/9.5/data/pg_hba.conf 修改如下内容，信任指定服务器连接 # IPv4 local connections: host    all            all      127.0.0.1/32      trust host    all            all      10.211.55.6/32（需要连接的服务器IP）  trust
> 
> ![](http://upload-images.jianshu.io/upload_images/2167535-922799b3ebdb5f58.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

远程连接配置完成，由于系统原因，还需要在防火墙中打开相应的端口。

> 9.打开防火墙 CentOS 防火墙中内置了PostgreSQL服务，配置文件位置在/usr/lib/firewalld/services/postgresql.xml，我们只需以服务方式将PostgreSQL服务开放即可。 firewall-cmd --add-service=postgresql --permanent  开放postgresql服务 firewall-cmd --reload  重载防火墙
> 
> ![](http://upload-images.jianshu.io/upload_images/2167535-051bf1d2d3fdd296.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后一步，不能忘记的，是重启数据库服务，使配置生效。

> 10\. 重启PostgreSQL数据服务 systemctl restart postgresql-9.5.service

至此，PostgreSQL 9.5 在CentOS 7上完成基本安装和配置。 相关链接：http://www.jianshu.com/p/7e95fd0bc91a http://www.linuxidc.com/Linux/2014-05/101787.htm http://www.mamicode.com/info-detail-1535571.html