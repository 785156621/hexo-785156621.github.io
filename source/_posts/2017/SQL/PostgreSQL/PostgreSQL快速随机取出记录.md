---
title: PostgreSQL快速随机取出记录
tags:
  - PostgreSQL
url: 222.html
id: 222
categories:
  - PostgreSql
date: 2017-09-13 11:38:16
---

1、传统的，也是最慢的方式： SELECT myid FROM mytable ORDER BY RANDOM() LIMIT 1; 缺点：近似于全表扫描，没有好的索引可以走； 2、稍微快一点的方式，用offset来实现： SELECT myid FROM mytable OFFSET floor(random()*N) LIMIT 1; 3、德哥的实现方式，用函数实现：

1.  digoal=> create or replace function f\_get\_random (i_range int) returns setof record as $BODY$
2.  digoal$> declare
3.  digoal$> v_result record;
4.  digoal$> v\_max\_id int;
5.  digoal$> v\_min\_id int;
6.  digoal$> v_random numeric;
7.  digoal$> begin
8.  digoal$> select random() into v_random;
9.  digoal$> select max(id),min(id) into v\_max\_id,v\_min\_id from tbl_user;
10.  digoal$> for v\_result in select * from tbl\_user where id between (v\_min\_id+(v\_random*(v\_max\_id-v\_min\_id))::int) and (v\_min\_id+(v\_random*(v\_max\_id-v\_min\_id))::int+i_range)
11.  digoal$> loop
12.  digoal$> return next v_result;
13.  digoal$> end loop;
14.  digoal$> return;
15.  digoal$> end
16.  digoal$> $BODY$ language plpgsql;
17.  CREATE FUNCTION

19.  以下举例取出10条连续的随机记录

21.  digoal=> select * from f\_get\_random(9) as (id bigint,firstname varchar(32),lastname varchar(32),corp varchar(32),age smallint);

4、借助另一列的索引实现：

1.  create table randtest (id serial primary key, data int not null);
2.  insert into randtest (data) select (random()*1000000)::int from generate_series(1,1000000);
3.  create index randtest\_md5\_id_idx on randtest (md5(id::text));
4.  explain analyze
5.  select * from randtest where md5(id::text)>md5(random()::text) order by md5(id::text) limit 1;

5、9.5版用 TABLESAMPLE:

1.  SELECT * FROM my_table TABLESAMPLE SYSTEM(0.000001) LIMIT 1;

原文链接：http://blog.chinaunix.net/uid-20332519-id-5616589.html