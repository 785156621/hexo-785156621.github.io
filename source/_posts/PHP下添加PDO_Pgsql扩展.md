---
title: PHP下添加PDO_Pgsql扩展
tags:
  - PostgreSQL
url: 288.html
id: 288
categories:
  - PostgreSql
  - SQL
date: 2017-05-04 10:13:08
---

进入[PHP](http://lib.csdn.net/base/php "PHP知识库")的源码安装包里（我用的是lnmp一键安装包目录在/root/lnmp1.3-full/src/php-5.6.22/)进入到ext/pdo\_pgsql目录，php源码包没有解压需解压（进入php源码包目录/root/lnmp1.3-full/src执行tar -zxvf php-5.6.22.tar.gz） 下面以本机环境为例： php-5.6.22的源码包放在:/root/lnmp1.3-full/src/php-5.6.22 编译pdo\_pgsql扩展 # cd /root/lnmp1.3-full/src/php-5.6.22/ext/pdo\_pgsql # /usr/local/php/bin/phpize # ./configure –with-php-config=/usr/local/php/bin/php-config # make # make install 安装完毕后在php.ini配置文件中的添加扩展路径中 # cp /usr/local/php/lib/php/extensions/no-debug-non-zts-20100525/pdo\_pgsql.so /usr/local/php/etc/ext/ 设置php扩展路径 # vi /usr/local/php/etc/php.ini 将extension\_dir设置成为如下值： extension\_dir = “/usr/local/php/etc/ext”       （如报错可不改） 添加扩展名称 extension=pdo_pgsql.so 如 ![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504101805.png) 重启ngix 至此完成php扩展的安装 注意： 1、执行“# ./configure –with-php-config=/usr/local/php/bin/php-config”步骤时如果出现如下错误提示, 需要执行该命令“# yum install postgresql-devel”安装postgresql开发版。 错误提示： checking for PostgreSQL support for PDO… yes, shared checking for pg_config… not found configure: error: Cannot find libpq-fe.h. Please specify correct PostgreSQL installation path by [woiit.net](http://www.woiit.net/) 2、 ![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504100708.png) 注：pgsql操作同上，pgsql.so和pdo_pgsql.so位置在/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226 安装成功后在phpinfo中可以看到： ![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504102110.png) 相关链接： http://blog.csdn.net/kelonsen/article/details/9116573 http://blog.csdn.net/bqw2008/article/details/51182261 https://bbs.vpser.net/viewthread.php?tid=12679&highlight=pgsql https://bbs.vpser.net/viewthread.php?tid=13731&highlight=postgresql https://bbs.vpser.net/viewthread.php?tid=13779&highlight=postgresql ttps://bbs.vpser.net/viewthread.php?tid=2049&highlight=postgresql