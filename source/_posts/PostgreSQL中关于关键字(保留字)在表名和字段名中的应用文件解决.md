---
title: PostgreSQL中关于关键字(保留字)在表名和字段名中的应用文件解决
tags:
  - PostgreSQL
url: 109.html
id: 109
categories:
  - PostgreSql
  - SQL
date: 2017-08-09 17:40:46
---

标识符和关键词

受限标识符或被引号修饰的标识符。它是由双引号（"）包围的一个任意字符序列。一个受限标识符总是一个标识符而不会是一个关键字。因此"select"可以用于引用一个名为“select”的列或者表，而一个没有引号修饰的select则会被当作一个关键词，从而在本应使用表或列名的地方引起解析错误。在上例中使用受限标识符的例子如下：UPDATE "my_table" SET "a" = 5;

在PostgreSQL关系型数据库中存在关键字的使用的问题，例如user 做表名,create table user (id int, name,varchar(20));创建的时候需要给表名user加上双引号"user";