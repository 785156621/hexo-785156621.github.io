---
title: 'pgsql使用记录:语法-查询字段大小写问题'
tags:
  - PostgreSQL
url: 83.html
id: 83
categories:
  - PostgreSql
  - SQL
date: 2017-07-31 10:38:42
---

下列说明来自网上文档： 有些命令以一个 SQL 标识的名称（如，一个表名）为参数。 这些参数遵循 SQL 语法关于双引号的规则： 不带双引号的标识强制成小写， 而双引号保护字母不受大小写转换，并且允许在标识符中使用空白。 在双引号中，成对的双引号在结果名字中分析成一个双引号。比如， FOO"BAR"BAZ 解析成fooBARbaz，而 "A weird"" name" 变成 A weird" name。 1.根据上述说明，我们来写点sql进行测试： select id as areaId,name from area where pid = '0' ![](http://gdmizi.com/wp-content/uploads/2017/07/QQ截图20170731103343.png) 2.加引号之后 select id as "areaId",name from area where pid = '0' ![](http://gdmizi.com/wp-content/uploads/2017/07/QQ截图20170731103457.png) 仔细观察表头的字段名，就可以发现其区别。 结合php的PDO设置，可以指定返回字段名字大小写规则 PDO::ATTR\_CASE：强制列名为指定的大小写。 PDO::CASE\_LOWER：强制列名小写。 PDO::CASE\_NATURAL：保留数据库驱动返回的列名。 PDO::CASE\_UPPER：强制列名大写。