---
title: 如何在linux中安装navicat112
tags:
  - SQL
url: 61.html
id: 61
categories:
  - SQL
date: 2017-07-21 10:15:02
---

一、去官网下载navicat112\_premium\_cs\_x64 for linux版本 二、用tar解压安装包 三、navicat解压即可用，直接进入解压后的目录，然后用‘./’运行./start\_navicat 四、navicat需要注册，如不注册只有大概10天左右的使用时间，解决方法是：删除在安装用户的家目录下的.navicat64目录 查看隐藏文件 ls -a plat@node1:~$ rm -rf .navicat64/ 再用‘./’运行./start\_navicat 此时你会发现，10天的使用时间会从当前时间开始算。 五、解决navicat界面显示乱码的问题 用‘./’运行start\_navicat之前，用vim编辑器打开start\_navicat文件，会看到 export LANG="en\_US.UTF-8" 将这句话改为 export LANG="zh_CN.UTF-8"。 再次运行，界面显示正常。