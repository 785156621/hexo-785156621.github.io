---
title: '[CentOs7]搭建ftp服务器'
tags:
  - centos7
url: 281.html
id: 281
categories:
  - CentOS
  - Linux
date: 2017-05-31 16:10:06
---

### 摘要

vsftpd 是“very secure FTP daemon”的缩写，安全性是它的一个最大的特点。vsftpd 是一个 UNIX 类操作系统上运行的服务器的名字，它可以运行在诸如 Linux、BSD、Solaris、 HP-UNIX等系统上面，是一个完全免费的、开放源代码的ftp服务器软件，支持很多其他的 FTP 服务器所不支持的特征。比如：非常高的安全性需求、带宽限制、良好的可伸缩性、可创建虚拟用户、支持IPv6、速率高等。 vsftpd是一款在Linux发行版中最受推崇的FTP服务器程序。特点是小巧轻快，安全易用。（来自百度百科）

### 安装vsftpd

1、检测是否已经安装vsftpd。

rpm -qa | grep vsftpd

![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161113193522983-1122453992.png) 如上图所示，并没安装vsftpd的任何版本。那么下面我们就搭建一个ftp 2、安装

yum -y install vsftpd

![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161113193628186-56053842.png) 启动vsftpd服务 systemctl start vsftpd.service 3、启动服务，检测是否安装成功

service vsftpd status

![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161113194059264-1981790179.png) 使用检测服务状态，running状态，说明服务已经启动。 4、匿名访问测试 可以在windows上使用ftp客户端进行连接，如图 ![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161113204626249-1344737316.png) vsftpd默认是开启匿名访问的，可以通过匿名的方式进行测试 ![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161113204734842-1204617869.png)

### 总结

可以通过匿名的方式访问ftp服务器了，说明已经安装成功了。下一步就是根据需要修改ftp的配置了。

### vsftpd添加用户

FTP用户一般是不能登录系统的,只能进入FTP服务器自己的目录中,这是为了安全.这样的用户就叫做虚拟用户了.实际上并不是真正的虚拟用户,只是不能登录SHELL了而已,没能力登录系统. 添加用户命令

/usr/sbin/adduser -d /opt/test_ftp -g ftp -s /sbin/nologin wolfyftp

上面的命令是添加一个 名称为 wolfyftp的用户。 命令解析：使用命令(adduser)添加wolfyftp用户,不能登录系统(-s /sbin/nologin),自己的文件夹在(-d /opt/test_ftp)),属于组ftp(-g ftp). 有用户了，然后为该用户设置密码

passwd wolfyftp

这里设置的密码为：123456 ![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161116135656498-1513945546.png) 密码添加成功 重启服务

/sbin/service vsftpd restart

![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161116135804060-593658275.png) 测试用户 使用xftp客户端进行访问，输入用户名和密码 ![](http://images2015.cnblogs.com/blog/511616/201611/511616-20161116140011763-1164080772.png) 安装vsftpd 1、源码安装 2、Yum 源安装 这里用的第2种方式，配制原理都是一样的，安培过程很简单，这里有几点是配制需要注意的 a 、如下图安装vsftp ![](http://img.blog.csdn.net/20150820181122940?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center) b、打开/etc/vsftpd如下图 ![](http://img.blog.csdn.net/20150820181412151?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center) c、如下配制需要修改的   vi vsftpd.conf 1、把任何人都可以访问修改为anonymous\_enable=NO 2、添加一句话在里面  userlist\_deny=NO   意思是只有user_list这里面的用户可以登陆ftp 3、相反的是 ftpusers这里用户都不允许登陆 4、添ftp用户并指定‘目录’  useradd -d /usr/local/apache/htdocs -s /sbin/nologin ftpuser  5、给ftpuser这个用户添加一个密码 passwdftpuser 6、在user_list文件里面添加上ftpuser这个用户 7、重启vsftpd  service vsftpd restart 8、此时vsftpd基本可以用了，下篇写一下权限问题 一、让ftp的用户只能访问自己的目录，即对其它目录无操作权限 1、打开配制文件  vi /etc/vsftpd/vsftpd.conf anonymous\_enable=NO #关闭匿名登陆 2、允许本地帐号登陆 local\_enable=YES #允许本地帐号登陆 3、不允许FTP用户切换根目录 chroot\_local\_user=YES#把前面的注释去除了 4、允许FTP用户拥有写的权限 allow\_writeable\_chroot=YES#在末尾添加这句话 5 重新启动vsftpd service vsftpd restart 二、只能用FTP登陆，不允许Telnet远程登陆 1、usermod -s /sbin/nologin ftpuser    (限制用户ftpuser1只可以ftp） 2、usermod -s /sbin/bash ftpuser        (如果需要，解除限制) 3、usermod -d /home/www/ ftpuser    (更改用户ftpuser1的主目录为www) 相关链接：http://www.cnblogs.com/wolf-sun/p/6058501.html http://www.cnblogs.com/wolf-sun/p/6069253.html http://blog.csdn.net/u013032788/article/details/47811885 http://blog.csdn.net/u013032788/article/details/47830979 http://blog.chinaunix.net/uid-22141042-id-1789633.html