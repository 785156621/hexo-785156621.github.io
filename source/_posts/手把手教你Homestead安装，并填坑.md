---
title: 手把手教你Homestead安装，并填坑
tags:
  - Laravel
  - Vagrant
url: 265.html
id: 265
categories:
  - Laravel
  - PHP
  - Vagrant
date: 2017-12-12 14:31:33
---

**话说作为laravel的开发者，你听说Homestead应该很久了，可是官方推荐的开发环境在国内为什么鲜有人用？我这几天试着安装了一下，发现官方的安装教程实在存在着太多的大坑，尤其让刚刚入道的开发者望而却步，在本文我试着手把手教大家填上这个坑.**

第一步 安装必须的软件
-----------

1.安装vagrant，[点此进入](https://link.jianshu.com?t=https://www.vagrantup.com/downloads.html)下载页，vagrant属于跨平台应用，我的系统是win10。关于[vagrant教程](https://link.jianshu.com?t=http://ninghao.net/blog/1566)，可以自己看一下，百度一下遍地是。不看也没关系，本文大概只用到其中的几个命令。 2.安装Virtualbox，当然你安装Vmware或parallels（OX系统）也可以，但后面下载的box要注意对应，虚拟机对应的版本不同。

第二步 导入box
---------

> vagrant box add laravel/homestead

**第一个坑：**原本只要如上的命令即可，但由于国内众所周知的网络原因，我们不得不考虑先下载好你需要的box再来添加。 首先在[hashicorp](https://link.jianshu.com?t=https://atlas.hashicorp.com/laravel/boxes/homestead/)中找到合适的版本,再在链接后加上”版本号/providers/虚拟机类型.box”即可获得下载链接. 如我们要下载最新的版本号为1.0.1的virtualbox版的box文件,链接即为:[https://atlas.hashicorp.com/laravel/boxes/homestead/versions/1.0.1/providers/virtualbox.box](https://link.jianshu.com?t=https://atlas.hashicorp.com/laravel/boxes/homestead/versions/0.4.1/providers/virtualbox.box) 由于国外链接下载太慢，这里提供了百度网盘链接（**_已更新到4.0.0_**）： 链接：[https://pan.baidu.com/s/1c2trJhA](https://pan.baidu.com/s/1c2trJhA) 密码：52ut 不建议采用迅雷离线下载，据说会导致下载的文件损坏！ 接下来我新建了一个文件夹名为homestead，然后我将下好的box重命名为homestead.box放入，然后在此文件夹内运行如下命令（这里是按照一些普通的教程来添加，这时候挖了一个坑，后面填上）。

> vagrant box add laravel/homestead homestead.box

接着运行

> vagrant box list

![](//upload-images.jianshu.io/upload_images/943143-d969ac03ec21a352.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/301)

vagrant box list

发现这个box已经添加进来就ok了。

第三步 下载官方homestead配置
-------------------

1）回到用户Home目录，从git上复制一份文件。失败了删除Homestead文件夹再试。 成功后，将会放在："C:\\Users\\<用户名>\\" 目录下面，我这里是：C:\\Users\\huang 依次输入：

> cd ~ git clone https://github.com/laravel/homestead.git Homestead

 

2）初始化homestead配置文件，执行bash init.sh将会在用户Home目录下生成.Homestead.yaml文件。 依次输入：

> cd ~/Homestead bash init.sh

![](http://gdmizi.com/wp-content/uploads/2017/12/QQ截图20171212142555-300x256.png)

 

第四步 配置Homestead.yaml
--------------------

**设置 IP及Provider** Homestead.yaml文件中的provider键表示使用哪个 Vagrant 提供者：virtualbox、vmware\_fushion或者vmware\_workstation，你可以将其设置为自己喜欢的提供者： ip: "192.168.10.10" provider: virtualbox **配置共享文件夹** Homestead.yaml文件中的folders属性列出了所有主机和 Homestead 虚拟机共享的文件夹，一旦这些目录中的文件有了修改，将会在本地和 Homestead 虚拟机之间保持同步，如果有需要的话，你可以配置多个共享文件夹（一般一个就够了）：

> folders: - map: D:/homestead/code  #（这是我本地的文件夹） to: /home/vagrant/Code

**配置 Nginx 站点** 对 Nginx 不熟？没问题，通过sites属性你可以方便地将“域名”映射到 Homestead 虚拟机的指定目录，Homestead.yaml中默认已经配置了一个示例站点。和共享文件夹一样，你可以配置多个站点：

> sites: - map: liang.app to: /home/vagrant/Code/Laravel/public

**Hosts文件** 不要忘记把 Nginx 站点配置中的域名添加到本地机器上的hosts文件中，该文件会将对本地域名的请求重定向到 Homestead 虚拟机，在 Mac 或 Linux上，该文件位于/etc/hosts，在 Windows 上，位于C:\\Windows\\System32\\drivers\\etc\\hosts，添加方式如下： 192.168.10.10 liang.app 确保 IP 地址和你的Homestead.yaml文件中列出的一致，一旦你将域名放置到hosts文件，就可以在浏览器中通过该域名访问站点了： http://liang.app

第五步 启动vagrant
-------------

在 Homestead 目录下运行vagrant up命令，Vagrant 将会启动虚拟机并自动配置共享文件夹以及 Nginx 站点。官方文档对此描述的如此这般简单，其实这里遇到了**第二个大坑** 我们输入vagrant up看会发生什么？一堆的错误提示！！！！

![](//upload-images.jianshu.io/upload_images/943143-00d73ba10d7e8f8e.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

我们根据提示，貌似是ssh的key没有生成，于是我们要运行如下命令，这个命令可以在git bash下生成，也可以在cmder等命令行工具完成，但在win下的cmd却无法执行。win 下可考虑powershell。

> ssh-keygen

好了，我们欢喜的以为，我们可以顺利运行了。vagrant up。我擦居然提示这个box没有，需要安装。出现了**第三个坑**

![](//upload-images.jianshu.io/upload_images/943143-567860dc9615e19a.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

再次出现该box不存在

导致该坑的原因，我们看之前的vagrant box list，里面显示laravel/homestead (virtualbox, 0)，而homestead要求Box Version: >= 1.0.0，这就不奇怪了。但我们明明下的是这个1.0.1版本啊。

![](//upload-images.jianshu.io/upload_images/943143-d969ac03ec21a352.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/301)

vagrant box list

#### 我们有两种方式修复这个大坑

#### 方式一

  修改homestead/scripts/homestead.rb的这个文件，将其中的>= 1.0.0改为< 1.0.0即可满足要求。但我并不推荐这种方式，因为实质对满足要求进行了篡改。

![](//upload-images.jianshu.io/upload_images/943143-7874000b3cb82cdc.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/552)

homestead.rb

#### 方式二

我们在homestead下新建一个名为homestead.json的一个json配置文件

> { "name": "laravel/homestead", "versions": \[{ "version": "1.0.1", "providers": \[{ "name": "virtualbox", "url": "F:/Vagrant/homestead/homestead.box" }\] }\] }

其中url是下载的homestead.box的路径 看懂了吗？接着我们运行这个命令

> vagrant box add homestead.json

![](//upload-images.jianshu.io/upload_images/943143-8eb820d308810180.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

已经添box成功

真的不容易啊，添加成功了 我们接着运行vagrant up试试

![](//upload-images.jianshu.io/upload_images/943143-021dccf8f037a53c.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/663)

成功运行

经过这样一番折腾终于成功运行了。

第六步 登录vagrant并安装laravel
-----------------------

这一步应该是我们的最后一步了，我们期待目标通过本地能够访问到你用vagrant搭建起来的laravel。我们通过vagrant ssh命令即可顺利登录我们的系统了。 由于设置上我们的vagrant虚拟机Code目录和我们的本地主机D:/homestead/Code是同一个目录，因此，我们先移步到该目录。 **第四个坑**出现了，我们一般是通过composer来进行安装，但出于GFW原因，我们不得不用[中国镜像](https://link.jianshu.com?t=http://pkg.phpcomposer.com/)来安装。vagrant虚拟机中运行如下命令

> composer config -g repo.packagist composer https://packagist.phpcomposer.com

接着我们通过composer来安装一个5.2版本 composer create-project laravel/laravel=5.2.* --prefer-dist OK，访问liang.app，出现了Laravel 5的欢迎界面，大功告成。 **补坑：**对于部分用户，可能出现autoload或boostrap不存在，说明依赖安装不完整，可以在laravel目录下运行如下命令来解决。

> composer update--no-scripts

由于直接git clone 官方在github上的东西可能造成与本box版本不一致，建议解决方案参考评论中beyond__devil所用的方法，将版本回滚。或者直接下最新的box或等我的box更新。  

原文链接：http://www.jianshu.com/p/ae9d1261bbd8 相关链接：http://laravelacademy.org/post/7658.html https://jingyan.baidu.com/article/48a42057fe2195a924250433.html https://segmentfault.com/q/1010000004354810/a-1020000004363813 后记：经历了各种坑百度了各种方法，最终终于安装成功。