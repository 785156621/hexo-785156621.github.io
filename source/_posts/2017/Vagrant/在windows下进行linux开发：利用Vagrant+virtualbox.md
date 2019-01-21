---
title: 在windows下进行linux开发：利用Vagrant+virtualbox
tags:
  - Vagrant
url: 250.html
id: 250
categories:
  - Vagrant
date: 2017-12-12 10:07:17
---

### 1，介绍Vagrant

我们做web开发的时候经常要安装各种本地测试环境，比如apache,php,mysql,redis等等。出于个人使用习惯，可能我们还是比较习惯用windows。虽然说在windows下搭建各种开发环境是可行的，各大开发环境都有windows版本。然而在windows下配置有时候会显得繁琐，并且还会导致开发环境（windows）和生产环境（lunix）不一致。 能不能在windows下也像linux那样开发？也许你想到了，用虚拟机。用虚拟机装个linux系统就好了。装完linux系统就设置共享目录，设置网络端口映射，等等。好像也有那么点繁琐。 还有，假如我们是一个团队进行开发，那么每个人的电脑上都要装个虚拟机\+ linux系统+各种运行环境。手动设置麻烦不说，大家的开发环境不太一致（可能你装了apcahe我装了nginx等），也是头疼。能不能把各种设置都自动化，并且保持整个团队的开发环境一致呢？ Vagrant就是为了解决这个问题而生的。它使用开源 VirtualBox 作为虚拟化支持，可以轻松的跨平台部署。

### 2，下载

下载VirtualBox：[http://download.virtualbox.org/virtualbox/5.2.2/VirtualBox-5.2.2-119230-Win.exe](http://download.virtualbox.org/virtualbox/5.2.2/VirtualBox-5.2.2-119230-Win.exe) 上面给出的是5.2.2版本的下载链接。要下载其他版本请访问官网[https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) 下载Vagrant：[https://releases.hashicorp.com/vagrant/2.0.1/vagrant\_2.0.1\_x86\_64.msi?\_ga=2.92704287.362862624.1512962307-1615333745.1510288662](https://releases.hashicorp.com/vagrant/2.0.1/vagrant_2.0.1_x86_64.msi?_ga=2.92704287.362862624.1512962307-1615333745.1510288662) 上面给出的是2.0.1版本win64位的下载链接。要下载其他版本请访问官网 [http://www.vagrantup.com/downloads.html](http://www.vagrantup.com/downloads.html) 下载虚拟镜像： [https://github.com/tommy-muehle/puppet-vagrant-boxes/releases/download/1.0.0/centos-6.6-x86_64.box](https://github.com/tommy-muehle/puppet-vagrant-boxes/releases/download/1.0.0/centos-6.6-x86_64.box) 上面给出的是centos-6.6镜像下载链接，要下载其他镜像请访问官网

*   官方仓库：[https://atlas.hashicorp.com/boxes/search](https://atlas.hashicorp.com/boxes/search)
*   官方镜像：[https://vagrantcloud.com/boxes/search](https://vagrantcloud.com/boxes/search)
*   第三方仓库：[http://www.vagrantbox.es/](http://www.vagrantbox.es/)

### 3，安装

下载好上面的软件包后，先安装VirtualBox,然后安装Vagrant。都是双击即可安装的，所以没什么好介绍。下面介绍下怎么把镜像导入。 先新建一个工作目录 比如我新建了D:VagrantWorkcentos-6.6-x86_64 打开cmd命令提示符，进入新目录，以我上面的目录为例，输入

            D:
            cd D:VagrantWorkcentos-6.6-x86_64
    

然后输入命令初始化 `vagrant init centos6.6` 把下载的centos-6.6-x86\_64.box复制到本目录D:VagrantWorkcentos-6.6-x86\_64下，执行 `vagrant box add centos6.6 centos-6.6-x86_64.box` 检查是否导入成功 `vagrant box list`

### 4，配置

用文本编辑器打开D:VagrantWorkcentos-6.6-x86_64目录下的Vagrantfile文件便可以进行一些常用配置。 下面列举出几个常用的配置。要用到其他配置请访问官网文档或者百度谷歌一下。 1，端口映射 `config.vm.network :forwarded_port, guest: 80, host: 8080` 把上面这句代码前面的#号去掉。它表示映射本机的8080端口到虚拟机的80端口 2，如果需要自己自由的访问虚拟机，但是别人不需要访问虚拟机，可以使用private_network，并为虚拟机设置IP。 `config.vm.network :private_network, ip: 192.168.33.10` 把上面这句代码前面的#号去掉即可 3，目录映射 `config.vm.synced_folder "D:/www", "/var/www/html"` 如果启用上面的命令，表示把本机的data目录共享到虚拟机里的/var/www目录

### 5，启动

进入目录D:VagrantWorkcentos-6.6-x86_64后执行命令 `vagrant up` 虚拟机启动之后则可以通过 vagrant ssh 联入虚拟机进行进一步的环境配置，或者软件安装相关的工作，在Windows系统下，并不能直接通过 vagrant ssh 连到虚拟机，需要使用 Putty，Xshell 等第三方工具进行连接。连接地址127.0.0.1，端口2222。登录的帐号root的密码为 vagrant

### 6，导出

在cmd里进行工作目录后，执行下面命令 `vagrant package --output centos-6.6.box` 完成后会在当前目录就会生成package.box，之后新建虚拟机则可使用这个box。如果事先在你的虚拟机里建立好了各种开发环境，那么你直接把这个box给你的团队其他成员安装，这样就可以省去一台台电脑部署的时间，还可以保持开发环境一致。很方便有木有。

### 7，其他命令

下面列举出一些常用的cmd操作命令 vagrant up （启动虚拟机） vagrant halt （关闭虚拟机——对应就是关机） vagrant suspend （暂停虚拟机——只是暂停，虚拟机内存等信息将以状态文件的方式保存在本地，可以执行恢复操作后继续使用） vagrant resume （恢复虚拟机 —— 与前面的暂停相对应） vagrant box remove centos6.6 （移除box，其中centos6.6是box名） vagrant destroy （删除虚拟机，删除后在当前虚拟机所做进行的除开Vagrantfile中的配置都不会保留）

### 8，常见问题

执行vagrant up时报以下错误： 解决方法： `vagrant plugin install vagrant-vbguest` `vagrant reload`

相关链接：http://blog.star7th.com/2015/06/1538.html 
http://blog.csdn.net/yjk13703623757/article/details/70040797 
http://blog.csdn.net/demon3182/article/details/51436032
http://www.jb51.net/article/121766.htm