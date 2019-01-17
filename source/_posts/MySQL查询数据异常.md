---
title: MySQL查询数据异常
tags:
  - MySQL
url: 278.html
id: 278
categories:
  - MySQL
  - SQL
date: 2017-05-13 14:03:59
---

SQLSTATE\[42000\]: Syntax error or access violation: 1055 Expression #1 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'www.handpark.cn.tp\_integral\_record.id' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql\_mode=only\_full\_group\_by 解决方法： 在 /etc/my.cnf 文件里加上如下： \[mysqld\] sql\_mode='NO\_ENGINE_SUBSTITUTION' 然后，重启Mysql服务就可以解决了！