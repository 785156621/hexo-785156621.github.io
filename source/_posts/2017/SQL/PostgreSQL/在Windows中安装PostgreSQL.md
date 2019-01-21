---
title: 在Windows中安装PostgreSQL
tags:
  - PostgreSQL
url: 287.html
id: 287
categories:
  - PostgreSql
  - SQL
date: 2017-05-04 13:22:39
---

下载安装包
-----

Enter片DB公司提供了PostgreSQL安装程序的下载。下载地址：[http://www.enterprisedb.com/products-services-training/pgdownload](http://www.enterprisedb.com/products-services-training/pgdownload) [http://www.postgres.cn/download](http://www.postgres.cn/download) 选择合适的版本进行下载。安装程序的名字类似于postgresql-9.6.2-1-windows-x64.exe。 ![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504120249.png)

安装PostgreSQL
------------

### 1.下载好后，双击安装程序进行安装。

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504122222.png)

### 2\. PostgreSQL安装位置

你可以选择你的PostgreSQL安装路径。默认的安装路径为C:\\Program Files\\PostgreSQL\\9.6（我的安装路径在D:\\PostgreSQL\\9.6）

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504122347.png)

### 3.数据库目录设置页面

这一步，你可以选择你的PostgreSQL数据存放的路径。默认的存放路径为C:\\Program Files\\PostgreSQL\\9.6\\data。（我的路径为D:\\PostgreSQL\\9.6\\data）

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504122615.png)

### 4\. 点击下一步，进入填写密码页面

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504122734.png)我设置的密码为123456

### 5\. 点击下一步，安装向导要求你填入服务监听的端口

和UNIX一样，默认端口为5432，你也可以设置任何你想使用的端口

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504122844.png)

### 6\. 设置新数据库的区域

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504123010.png)我选的是默认的

### 7.选择恰当的区域，点击下一步，向导图示将开始安装数据库。在点击下一步，如果不出错，安装过程将进行并正常完成。

![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504123226.png)

### 8.完成安装

### ![](http://huanggd.com/wp-content/uploads/2017/05/QQ截图20170504123708.png)把勾去掉

相关链接：[http://www.cnblogs.com/sharpest/p/6225028.html](http://www.cnblogs.com/sharpest/p/6225028.html)