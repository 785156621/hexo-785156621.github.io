---
title: 'mount: unknown filesystem type ''vboxsf'''
tags:
  - Vagrant
url: 248.html
id: 248
categories:
  - Vagrant
date: 2017-12-11 14:35:04
---

vagrant无法与主机共享文件夹? ![](http://gdmizi.com/wp-content/uploads/2017/12/QQ图片20171211143055.png) 这个问题解决方案已经知道。其实很简单，就是缺一个插件，装上就ok `vagrant plugin install vagrant-vbguest` 然后  `vagrant reload`  问题解决。   相关链接：http://blog.csdn.net/demon3182/article/details/51436032 http://www.cnblogs.com/HansBug/p/7403306.html http://www.jb51.net/article/121766.htm