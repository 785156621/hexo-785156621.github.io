---
title: Linux-CentOS XAMPP Apache 启用GZIP压缩功能 mod_deflate的安装配置
tags:
  - PHP
url: 208.html
id: 208
categories:
  - PHP
date: 2017-09-08 14:23:58
---

**【1】概览** 许多网络服务器可以通过调用第三方模块或使用内置程序将文件压缩为GZIP格式，然后再发送该压缩文件以供下载。这样可以在下载呈现网站所需的资源时，为您节省一些时间。

*   减少高达70％的网页大小
*   提高网页速度
*   需要访问的.htaccess文件或者服务器管理文件

**什么是Gzip已压缩？** 当用户点击你的网站时，由您的服务器提供所要求的文件，这些文件越大，到你的浏览器并显示在屏幕上所需的时间就越长.GZIP在传输他们到浏览器之前压缩您的网页和样式表，这大大减少了传输时间，因为这些文件小得多.GZIP压缩是网页速度优化的基本方法，现在绝大多数网站都已经启用GZIP。 **GZIP是怎样工作的？** GZIP实际上是一个相当简单的想法，但是善加利用是非常强大的。GZIP把一个文本文件的字符串替换使整个文件大小更小。由于CSS文件和HTML文件使用了大量重复的文字，并有空白的字符，而GZIP压缩公用字符串，这可以减少页面和样式表的高达70％的大小！而对您的网络服务器启用Gzip已是相对简单的。当浏览器访问一个网页服务器时，会先检查看看是否有服务器启用GZIP，并请求该网页。如果启用，它就接收gzip的文件，否则它会接收未压缩的版本，但这页面大小将大得多。 **为什么这么重要** 压缩的GZip如此重要的主要的原因是，它减少了一个网站传输网页文件和样式表所需的时间，最终降低你的网站加载时间。 **【2】的Apache服务器配置** 你需要添加如下脚本到的.htaccess文件或者在http.conf的文件尾加上：

**\[纯\] **[查看纯](http://blog.csdn.net/aoshilang2249/article/details/52291423# "查看纯文本")[文本](http://blog.csdn.net/aoshilang2249/article/details/52291423# "复制")

[打印](http://blog.csdn.net/aoshilang2249/article/details/52291423# "打印")[？](http://blog.csdn.net/aoshilang2249/article/details/52291423# "？")

1.  编辑http.conf文件
2.  去掉#LoadModule headers\_module modules / mod\_headers.so前面的注释＃
3.  去掉#LoadModule deflate\_module modules / mod\_deflate.so前面的注释＃
4.  去掉#LoadModule filter\_module modules / mod\_filter.so前面的注释＃

**\[纯\] **[查看纯](http://blog.csdn.net/aoshilang2249/article/details/52291423# "查看纯文本")[文本](http://blog.csdn.net/aoshilang2249/article/details/52291423# "复制")

[打印](http://blog.csdn.net/aoshilang2249/article/details/52291423# "打印")[？](http://blog.csdn.net/aoshilang2249/article/details/52291423# "？")

1.  ＃压缩HTML，CSS，JavaScript，文本，XML和字体
2.  <IfModule mod_deflate.c>
3.      AddOutputFilterByType DEFLATE应用程序/ javascript
4.      AddOutputFilterByType DEFLATE应用程序/ rss + xml
5.      AddOutputFilterByType DEFLATE application / vnd.ms-fontobject
6.      AddOutputFilterByType DEFLATE应用程序/ x字体
7.      AddOutputFilterByType DEFLATE应用程序/ x-font-opentype
8.      AddOutputFilterByType DEFLATE应用程序/ x-font-otf
9.      AddOutputFilterByType DEFLATE应用程序/ x-font-truetype
10.      AddOutputFilterByType DEFLATE应用程序/ x-font-ttf
11.      AddOutputFilterByType DEFLATE应用程序/ x-javascript
12.      AddOutputFilterByType DEFLATE application / xhtml + xml
13.      AddOutputFilterByType DEFLATE application / xml
14.      AddOutputFilterByType DEFLATE应用程序/ x-httpd-php
15.      AddOutputFilterByType DEFLATE应用程序/ x-httpd-fastphp
16.      AddOutputFilterByType DEFLATE字体/ opentype
17.      AddOutputFilterByType DEFLATE字体/ otf
18.      AddOutputFilterByType DEFLATE font / ttf
19.      AddOutputFilterByType DEFLATE image / svg + xml
20.      AddOutputFilterByType DEFLATE image / x-icon
21.      AddOutputFilterByType DEFLATE文本/ css
22.      AddOutputFilterByType DEFLATE text / html
23.      AddOutputFilterByType DEFLATE text / javascript
24.      AddOutputFilterByType DEFLATE text / plain
25.      AddOutputFilterByType DEFLATE text / xml
26.      ＃删除浏览器错误（只有真正的旧浏览器需要）
27.      BrowserMatch ^ Mozilla / 4 gzip-only-text / html＃Netscape 4.x有一些问题，所以只压缩文件类型是text / html的
28.      BrowserMatch ^ Mozilla / 4 \ .0 \[678\] no-gzip＃Netscape 4.06-4.08有更多的问题，所以不开启压缩
29.      BrowserMatch \ bMSIE！no-gzip！gzip-only-text / html＃但IE浏览器会伪装成Netscape，是事实上它没有问题
30.      #SetEnvIfNoCase Request_URI。（？：gif | jpe？g | png）$ no-gzip dont-vary＃设置不对后缀gif，jpg，jpeg，png的图片文件进行压缩
31.      头附加不同的用户代理
32.  </ IfModule>配置

**【3】常见问题** **怎么知道网站的GZip压缩压缩是否起作用了？** 使用webkaka的[网站速度诊断](http://pagespeed.webkaka.com/)，在“优化建议”里可以看到网站各文件是否使用了GZip压缩。 **为什么图片，PDF和视频文件没有压缩？** GZip压缩压缩对图片，PDF，视频和其他已经使用二进制压缩过的文件是无效的。 **闪存被破坏** 闪光灯预加载器不能处理压缩的闪存文件，如果你已经压缩的闪存被破坏了，请不要压缩闪存文件。 **【4】建议** **把网页内容写得使压缩更有效** 为了使用你的网页内容得到更好的压缩，请参照如下方法： **1，确保HTML和CSS代码的一致性。为了实现一致性** 在可能的情况以相同的顺序指定CSS关键值，例如按字母顺序排列它们。以相同的顺序指定HTML属性，例如按字母顺序排列它们。把HREF第一个链接（因为它是最常见的），然后按字母顺序排列剩下的。例如，谷歌的搜索结果页面，当HTML属性是按字母顺序排列时，gzip的压缩过的输出的大小减少1.5％。保持字母的一致性，例如在任何时候都是小写。保持引号的一致性，例如全部使用单引号，或者全部使用双引号，又或者如果可能的话干脆连引号也不要。 **2，[优化CSS](http://pagespeed.webkaka.com/youhua/css/)和[优化Javascript](http://pagespeed.webkaka.com/youhua/js/)。** 优化CSS和Java脚本不仅可以帮助外部的CSS和Java脚本文件的压缩，还可以帮助HTML页面内嵌的CSS和Java脚本代码。 **不要使用GZip压缩压缩图片和其他二进制文件** 网页支持已经压缩过的图片文件，同样支持已经压缩过的视频，PDF等二进制文件;使用的GZip压缩这些文件，不会提供额外的好处，反而使他们的体积变得更大。   原文链接：[http://blog.csdn.net/aoshilang2249/article/details/52291423](http://blog.csdn.net/aoshilang2249/article/details/52291423)