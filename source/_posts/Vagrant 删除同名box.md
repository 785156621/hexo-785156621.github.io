---
title: Vagrant 删除同名box
tags:
  - Vagrant
url: 270.html
id: 270
categories:
  - Vagrant
date: 2017-12-12 15:44:37
---

box多版本共存的情况 如果box升级过，那么在box list中会出现两个同名，但版本不同的镜像。如：

> C:\\Users\\lanlin>vagrant box list centos/7 (virtualbox, 1710.01) laravel/homestead (virtualbox, 0) laravel/homestead (virtualbox, 4.0.0)

使用该镜像创建虚拟机的时候，默认会使用高版本的box。 如果想使用低版本，需要修改Vagrantfile,指定box-version 在config.vm.box=xxx下一行，如上面的例子中，在“config.vm.box = "laravel/homestead"”后面增加一行配置信息：config.vm.box_version = "4.0.0" 同样，如果想删除一个box，如下操作会失败：

> $ vagrant remove laravel-homestead You requested to remove the box 'laravel/homestead' with provider 'virtualbox'. This box has multiple versions. You must explicitly specify which version you want to remove with the `--box-version` flag or specify the `--all` flag to remove all versions. The available versions for this box are: * 0 * 4.0.0

这时有两个选择： `- vagrant box remove laravel-homestead --all` 删除所有同名镜像 `- vagrant box remove laravel-homestead --box-version=4.0.0` 删除指定版本的镜像