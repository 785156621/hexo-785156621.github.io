---
title: php mysql中如何往表中追加数据
tags:
  - MySQL
url: 231.html
id: 231
categories:
  - MySQL
  - SQL
date: 2017-09-29 16:49:18
---

网友回复:update table set field=concat(field, '072110003') where field='072110001'; 在两个号码中间用空格隔开，则可以用 update table set field=concat(' ', field, '072110003') where field='072110001'; 网友回复:这是固定字符串 我现在需要的是变量追加，意思是现在的072110001存放在一个变量中，网页上的一个表单中，如何追加？ 网友回复:update table set field=concat(' ', field, '换成一个变量') where field='072110001'; 这样不就可以了么？如果要追加多个，可以把SQL写入循环里． 网友回复:恩 不错 搞定了 等的接分吧 网友回复:说的清楚点~~~ 网友回复:汗，刚发现帖出来的sql里面有个地方错了。 update table set field=concat(' ', field, '072110003') where field='072110001'; 应该是 update table set field=concat\_ws(' ', field, '072110003') where field='072110001'; 或者 update table set field=concat(field, ' ', '072110003') where field='072110001'; 对于需要一次添加多个值，并且都用' '隔开的话，用第二条语句比较方便。 一次只用一个的话，concat比较简单而且不同数据库通用。 网友回复:在问一个相反的问题，如何从这个字段里去掉部分值， 比如说现在是“072110002 072110003”，我要去掉072110003或者是去掉072110002，应如何实现？ 应该也是用update吧，还是用delete? 网友回复:高手们，快帮下忙啊，谢谢了 ！！！ 网友回复:我不得不说，这样的表设计太………………了。 网友回复:现实需要，不得不设计成这样啊。这个问题我解决了。 问一个很奇怪的问题 ： 我在表单里输出了数据库中的一条记录，我改变了表单中输出的内容，怎么写不到数据库里了，始终改变不了里面的内容。我做的是修改功能，怎么修改不了？ 网友回复:update table set field=replace(field, '072110003', '') where field='072110001 072110003'   原文链接：http://blog.163.com/liang\_fujianyeah@126/blog/static/11592655220119193632193/