---
title: PostgreSQL远程连接配置
tags:
  - PostgreSQL
url: 275.html
id: 275
categories:
  - PostgreSql
  - SQL
date: 2017-07-13 12:20:59
---

postgresql默认情况下，远程访问不能成功，如果需要允许远程访问，需要修改两个配置文件，说明如下： 1.postgresql.conf 将该文件中的listen\_addresses项值设定为“*”，在9.0 Windows版中，该项配置已经是“*”,无需修改。 2.pg\_hba.conf 在该配置文件的host all all 127.0.0.1/32 md5行下添加以下配置，或者直接将这一行修改为以下配置 host    all    all    0.0.0.0/0    md5 如果不希望允许所有IP远程访问，则可以将上述配置项中的0.0.0.0设定为特定的IP值,比如： host  all    all    192.168.1.0/24    md5 host  all    all    192.168.1.0/32    trust 表示允许网段192.168.1.0上的所有主机使用所有合法的数据库用户名访问数据库，并提供加密的密码验证。 其中，数字24是子网掩码，表示允许192.168.1.0--192.168.1.255的计算机访问！