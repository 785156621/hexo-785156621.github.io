---
title: pgsql 关闭自动提交事务
tags:
  - PostgreSQL
url: 229.html
id: 229
categories:
  - PostgreSql
  - SQL
date: 2017-09-28 16:39:49
---

最早以前,  postgresql服务端有 autocommit开关, 然而又有语句 begin transaction 来控制事务, 这样可能会造成混乱, 比如 autocommit=on的情况下, 用begin transaction启动手工事务,此时autocommit到底是on 还是off? 后来干脆就取消autocommit开关, 只有一条命令begin transaction来管理事务, 越简单越不易混乱.