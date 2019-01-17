---
title: win10下安装php7redis扩展
tags:
  - Redis
url: 291.html
id: 291
categories:
  - Redis
date: 2017-04-28 18:13:57
---

一、工具准备 1. [Redis](http://lib.csdn.net/base/redis "Redis知识库") for windows 下载 [https://github.com/MSOpenTech/redis](https://github.com/MSOpenTech/redis) 2. [PHP](http://lib.csdn.net/base/36 "PHP知识库")扩展下载 [http://pecl.php.net/package-stats.php](http://pecl.php.net/package-stats.php) （redis 和 igbinary） [PHP](http://lib.csdn.net/base/php "PHP知识库") 7 扩展下载 [http://windows.php.net/downloads/pecl/snaps/redis/20160319/](http://windows.php.net/downloads/pecl/snaps/redis/20160319/) http://windows.php.net/downloads/pecl/releases/redis/3.1.2/ [注： 下载扩展是要注意看自己的php版本及x86orx64 和 compiler  编译版本](http://windows.php.net/downloads/pecl/snaps/redis/20160319/) 二、redis安装 1.redis安装 将下载后的redis文件解压到安装目录 2.redis启动 1).windows+R 然后 cmd 进入到D:\\program files\\redis（根据自己redis路径自行调整） 2).输入 redis-server.exe 点击回车，自己注意看一下redis目录下文件情况，不同版本的启动方式有点小差异。出现下图标识执行成功。**成功后别关闭当前窗口，操作redis期间都要保证此窗口打开，关闭此窗口表示 关闭reids，重新打开一个cmd** 3).cmd 进入到D:\\program files\\redis（根据自己redis路径自行调整） 然后输入 redis-cli.exe 点击回车。现在我们就可以做一些测试如下图，标识redis安装 启动成功。 **注：两个cmd窗口同时打开，之前开启redis的窗口不能关掉** 三、 php扩展 1.把下载到的php\_redis.dll和php\_igbinary.dll扩展文件 拷贝到php\\ext中 2. 打开php.ini；加入以下代码

1.  #php for redis
2.  extension=php_igbinary.dll
3.  extension=php_redis.dll

3.重启服务，phpinfo中有redis项表示成功 四.demo

1.  <span style="font-size:18px;">$redis = new redis();
2.  $redis->connect("127.0.0.1","6379");  //php客户端设置的ip及端口  
3.  //存储一个 值  
4.  $redis->set("type",12);
5.  echo $redis->get("type");

7.  //存储多个值  
8.  $array = array('first_key'=>'first_val',
9.      'second_key'=>'second_val',
10.      'third_key'=>'third_val');
11.  $array_get = array('first_key','second_key','third_key');
12.  $redis->mset($array);
13.  var_dump($redis->mget($array_get)); </span>

![](http://img.blog.csdn.net/20151210101815352?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center) **附：Redis类的一些属性及方法** ** a）连接redis server**

*   connect ：连接server
*   pconnect ：长连接
*   auth ：权限验证
*   select ：选择DB
*   close ： 关闭连接
*   setOption : 设置 client 选项
*   getOption ： 获取client选项
*   ping ： ping redis server
*   echo ： 输出字符串

注意，如果频繁操作redis，不停地connect 和close会很耗性能的，这个时候，建议用pconnect 建立个长连接 **b）字符串读写函数**

*   append  ：在值的后面追加值
*   decr ：递减一个key的值
*   incr ：递增一个key的值
*   get ：获取一个值
*   set ：设置一个值
*   getSet ：设置值，并返回老值
*   mGet ：批量获取值
*   mSet ：批量设置值
*   strlen ：获取值长度

注意：如果能用批量操作尽量用批量，减少频繁连接redis[数据库](http://lib.csdn.net/base/14 "MySQL知识库")性能 **c）hash读写函数**

*   hDel ：删除一个多个域
*   hExists ：判断一个hash域是否存在
*   hGet ：获取hash域的值
*   hGetAll ：获取所有域值
*   hIncrBy ：自增长一个hash int域的值
*   hKeys ：获取hash 所有域
*   hLen ：获取域个数
*   hMGet ：批量获取域的值
*   hMSet ：批量设置域的值
*   hSet ：设置域的值
*   hVals：得到所有域的值

**d）list读写函数**

*   lInsert：插入元素
*   lLen：list长度
*   lPop：移除并获取第一个颜色
*   lPush：插入一个元素
*   lRem：移除元素
*   lSet：设置元素值

**e）set**

*   sAdd：增加一个或多个成员
*   sIsMember：是否包含
*   sMembers：得到成员
*   sMove：移动成员
*   sPop：移除成员
*   sRandMember：得到随机成员
*   sRem：删除

**f）sorted set**

*   zAdd：增加一个或多个
*   zCard：成员个数
*   zIncrBy：递增成员score
*   zRange：返回索引范围内的成员
*   zRangeByScore ：返回score范围内的成员
*   zScore：获取成员score
*   zRem：移除一个或多个成员