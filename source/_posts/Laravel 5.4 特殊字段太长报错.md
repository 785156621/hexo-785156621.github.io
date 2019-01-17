---
title: 'Laravel 5.4: 特殊字段太长报错'
tags:
  - Laravel
  - PHP
url: 236.html
id: 236
categories:
  - Laravel
  - PHP
date: 2017-11-09 16:46:38
---

laravel 5.4 改变了默认的数据库字符集，现在utf8mb4包括存储emojis支持。如果你运行MySQL v5.7.7或者更高版本，则不需要做任何事情。 当你试着在一些MariaDB或者一些老版本的的MySQL上运行 migrations 命令时，你可能会碰到下面这个错误：

\[Illuminate\\Database\\QueryException\]
SQLSTATE\[42000\]: Syntax error or access violation: 1071 Specified key was too long; 
max key length is 767 bytes (SQL: alter table users add unique users\_email\_unique(email))

\[PDOException\]
SQLSTATE\[42000\]: Syntax error or access violation: 1071 Specified key was too long; 
max key length is 767 bytes

我们可以在 AppServiceProvider.php 文件里的 boot 方法里设置一个默认值：

<?php
namespace App\\Providers;

use Illuminate\\Support\\ServiceProvider;
use Illuminate\\Support\\Facades\\Schema;

class AppServiceProvider extends ServiceProvider
{
/\*\*
\* Bootstrap any application services.
\*
\* @return void
*/
public function boot()
{
Schema::defaultStringLength(191);
}

/\*\*
\* Register any application services.
\*
\* @return void
*/
public function register()
{
//
}
}

原文链接：[https://www.cnblogs.com/betx/p/6544090.html](https://www.cnblogs.com/betx/p/6544090.html)