---
title: Laravel笔记：指定表名的重要性
tags:
  - Laravel
  - PHP
url: 239.html
id: 239
categories:
  - Laravel
  - PHP
date: 2017-11-17 15:59:21
---

最近准备开始花一些自己的空余时间来学习一下PHP的框架，[爱鱼客](http://www.iyu.co/)在做了一些了解之后打算从Laravel框架开始学习，原因就是现在越来越多的人开始使用[Laravel框架](http://www.iyu.co/tag/Laravel)了。以后会时不时添加一些笔记以加深印象也便于日后查看。![laravel](http://cdn.iyu.co/wp-content/uploads/2017/01/laravel.jpg)

今日笔记：Laravel表名的指定
-----------------

由于Laravel在创建 `Model` 的时候会自动关联对应的表名，具体遇到问题的流程如下： 在Terminal中输入以下指令后会在 `App` 目录下创建一个`customer.php` 文件

    php artisan make:model Customer

但是这边默认需要在数据库中添加的表为 customers 而不是 customer，也就是说系统会自动根据 Model 的名称加上复数“s”，这边一般情况是没有问题，但是如果遇到诸如 person 变 people 或者各种我们国人不能很简单辨别的形式，那么实惠对我们的开发造成问题；另外也有可能我们不想要系统自动匹配数据库，而要对表名进行自定义。

我们需要做的其实很简单，在创建的 Model 文件函数中添加一条指定表名的规则：

    <?php

如上我们加入了 `protected $table = 'customer';`，强制把 `customer.php` 对应的数据库指定为 `customer`，而不是系统默认的 `customers`。这一点我们也可以在框架自带的User.php中看到，为了程序运行稳定和不出错，这一步应该在每一个`Model` 中都应用。   原文链接：http://www.iyu.co/web/laravel-protect-table/ ![](http://gdmizi.com/wp-content/uploads/2017/11/QQ截图20171117161904-1024x75.png) 我表名为category，但是转化为categories了，加s后也不行。所以最好还是要指定表名 相关链接：https://laravel-china.org/topics/201/table-name-with-the-class-name-in-the-plural-form-how-to-deal-with-irregular-nouns