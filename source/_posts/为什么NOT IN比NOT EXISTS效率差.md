---
title: 为什么NOT IN比NOT EXISTS效率差
tags:
  - PostgreSQL
url: 223.html
id: 223
categories:
  - PostgreSql
date: 2017-09-13 12:06:30
---

#### 为什么NOT IN效率差

两个SQL, 用NOT IN和NOT EXISTS两种不同写法,效率差别很大. 下面两种不同的写法，第一种跑了几个小时也没出结果，第二种几分钟就跑完了

select id from r where r.id not in (select id from tbl);
select id from r where not exists (select id from tbl where id = r.id);

早就听说过NOT IN效率差,今天才第一次认识到这个问题的本质 (以下以PostgreSQL来说明）

#### NOT IN和NOT EXISTS执行计划是不一样的

**NOT IN**

postgres=# explain select id from r where r.id not in (select id from tbl);
                               QUERY PLAN                                
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-
 Seq Scan on r  (cost=0.00..1905433091.42 rows=194644 width=7)
   Filter: (NOT (SubPlan 1))
   SubPlan 1
     -\>  Materialize  (cost=0.00..8850.78 rows=375385 width=7)
           -\>  Seq Scan on tbl  (cost=0.00..5506.85 rows=375385 width=7)
(5 rows)

**NOT EXISTS**

postgres=# explain select id from r where not exists (select id from tbl where id = r.id);
                              QUERY PLAN                               
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-
 Hash Anti Join  (cost=11666.16..40782.08 rows=13902 width=7)
   Hash Cond: ((r.id)::text = (tbl.id)::text)
   -\>  Seq Scan on r  (cost=0.00..20668.87 rows=389287 width=7)
   -\>  Hash  (cost=5506.85..5506.85 rows=375385 width=7)
         -\>  Seq Scan on tbl  (cost=0.00..5506.85 rows=375385 width=7)
(5 rows)

我们看到, NOT EXISTS会被重写成Hash Anti Join, 而NOT IN不会,由于子查询中的结果集比较大, 产生了Materialize Hash join, 把二个表按照join key放入hash table, 然后遍历第一个表,在hash table中查找到第一个表的join key, 如果找到, 返回一条结果 Anti Join, 对于第一个表里的记录,当在第二张表没有发现与之匹配记录时，才会返回记录 与Anti Join类似但有相反意义的是Semi Join, 即在两表关联时,只返回第二个表第一次匹配的记录;Anti Join可以用于生成in select的计划

#### Hash Anti Join更高效

以上两个执行计划, 后面的要比前面的更高效. 尤其是当子查询中的结果集比较大时, 需要产生Materialize, NOT IN效率恶化得更明显． 为什么这两个SQL生成计划是不一样的呢? 为什么不为NOT IN生成更优的计划, 就像NOT EXISTS一样? 实际上, 问题在于, 这两个SQL实际上有不同的语义.

#### NOT IN比较特殊的地方,在于NULL值的处理

create table  ta ( no int, str varchar(20));
create table  tb (no int, str varchar(20));
insert into  ta (no, str) values (1, 'a'), (2, 'b'), (3, 'c'), (4, 'd');
insert into tb(no, str) values (1, 'a'), (2, 'b'), (3, 'c'), (4, NULL);

下面的两个SQL是不等价的

select no, str from ta where str not in (select str from tb);
select no, str from ta where not exists (select str from tb where str = ta.str);

not in查询结果:

postgres=# select no, str from ta where str not in (select str from tb);
 no | str 
----+-----
(0 rows)

not exists查询结果:

postgres=# select no, str from ta where not exists (select str from tb where str = ta.str);
 no | str 
----+-----
  4 | d
(1 row)

或许和我们期望的结果不太一样 如果去掉子查询中的NULL, NOT IN和NOT EXISTS的结果就是相同的

postgres=# select no, str from ta where str not in (select str from tb where str is not null);
 no | str 
----+-----
  4 | d
(1 row)

如果IN list中有一个值为空, 那么整个查询的结果集就是空的 SQL标准规定, NULL的任何运算(除了类似IS NULL这种)都返回NULL 对于下面的SQL, 返回的结果集是空

select no, str from ta where str not in ( 'a', NULL); -- empty resultset

'd' not in ('a', NULL)返回值是NULL(不是True, 也不是False)

select 'd' not in ('a', NULL);  -- NULL

#### 结论：

由上面可以看出, NOT EXISTS比NOT IN效率更高, 是因为生成了更高效的执行计划 因为SQL标准对NULL的定义, NOT IN无法像NOT EXISTS那样生成更为高效的Hash Anti Join的计划 所以，以后应该尽量避免用NOT IN这种写法, 虽然想不通NOT IN对NULL处理的这种语义在现实中有什么意义^^   原文链接：http://blog.chinaunix.net/uid-29128384-id-4417450.html