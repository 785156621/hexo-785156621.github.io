---
title: 为什么datetime类型的值不能修改为null?
url: 95.html
id: 95
categories:
  - 未分类
tags:
---

为什么datetime类型的值不能修改为null?

我mysql表里面那有一个列pendingtime,数据类型是datetime,新增列时选择的type为timestamp,可以为空，默认为NULL,新增列后默认值为NULL. 我在php里面使用sql语句修改pendingtime为now()，pendingtime无意义的时候我再把它改为NULL,我直接使用sql语句也无法修改pendingtime为NULL,都提示： ERROR 1292 (22007): Incorrect datetime value: 'null' for column 'pendingtime'。 ------解决方案-------------------- 那是不行的！ mysql 在对 datetime 类型字段赋值时，有一个日期时间格式转换过程，如遇到非法的日期格式（比如 null）就会报错，你可以用'000-00-00 00:00:00'将他置空