---
title: PHP上传文件详解 错误提示
tags:
  - PHP
url: 171.html
id: 171
categories:
  - PHP
date: 2017-08-23 23:29:16
---

首先在php.ini里配置上载文件。有以下几个重要的配置单：

选项

默认值

说明

post\_max\_size

8M

控制以后的POST请求的最大规模。必须大于upload\_max\_filesize选项值。

max\_input\_time

60

指定一个POST请求提交所有数据可以花费的时间。以秒为单位。在此时间之后结束数据提交。

file_uploads

On

指出是否允许文件上传。默认值为on

upload\_max\_filesize

2M

控制PHP接受的最大文件规模。如果文件太大，PHP就写入一个0字节的占位符文件。

upload\_tmp\_dir

NULL

必须设置为一个有效目录。可以将上传的文件放在这里等候处理。

  然后，在表单HTML中设置文件上传。需要注意三个地方：

1.  1.       将form表单提交方式设为POST
2.  2.       添加一个“file”类型的新的标记<input>。
3.  3.       将enctype属性添加到表单中，表示将使用新的multipart/form-data MIME类型。

  当提交数据后，可以通过$\_FILES\[‘filename’\]来取得这个文件的信息。该信息如下： $\_FILES\[‘filename’\]： \[‘name’\]  =>   文件名 \[‘type’\]   =>   文件MIME类型。如image/jpeg, text/plain, application/octet-stream等。 \[‘tmp\_name’\] => 如果文件小于允许上传文件大小，则该位置表示上传的文件临时存放路径及临时文件名，被放在upload\_tmp_dir所指定的位置。 \[‘error’\] =>    错误代码。 \[‘size’\] =>      文件大小。 其中error错误代码可能的值如下表：

编码

值

说明

UPLOAD\_ERR\_OK

0

文件成功上传

UPLOAD\_ERR\_INI_SIZE

1

文件大小比php.ini中upload\_max\_filesize指定值要大

UPLOAD\_ERR\_FORM_SIZE

2

文件的小比表单的MAX\_FILE\_SIZE指定的值大

UPLOAD\_ERR\_PARTIAL

3

文件上传不完整（可能因为请求时间过长被终止）

UPLOAD\_ERR\_NO_FILE

4

没有文件随着这个请求上传

UPLOAD\_ERR\_NO\_TMP\_DIR

6

在php.ini中没有指定临时文件夹

只有当$\_FILES\[‘filename’\]\[‘error’\]的值为0时，才应该继续处理文件。   *************************************************************************************   在apache配置文件中设置php上传临时目录 在服务器上配置webmail(比如我最喜欢的SquirrelMail)时，出于服务器安全考虑，一般在apache配置文件中作 php\_admin\_value open\_basedir <path to web root> 的限制，防止php程序浏览整个硬盘，这个限制在使用虚拟主机的服务器上使用的更多。 然 而这个安全措施带来一个隐含的限制，就是php的上传临时目录(默认为/tmp)无法被php程序访问，导致webmail中上传附件时失败，比如 SquirrelMail提示“Could not move/copy file. File Not Attached.”(“无法移动/复制文件。文件需要被附在邮件上”)。 通过在apache配置文件中添加一个设置 php\_admin\_value upload\_tmp\_dir <path to temp dir> 让php程序在上传时使用指定的目录作为临时文件目录。 当然，要注意此目录的权限设置要让apache的运行用户能写入。 学习PHP难免总是会遇到一些莫名其妙的问题，就是搞不懂为什么，明明自己设置的都是正确的，但就是出问题，这不，今天我又遇到了一个这样的问题，浪费了我好几个小时，才弄明白是哪里出了问题，真是郁闷死了。 今天直接找了一个上传文件的php源代码进行测试，总是显示错误，提示为错误代码是2。我就在网上找了找资料。 **<!--使用POST上传文件示例：upload\_file\_post.php----------------------------> <form enctype="multipart/form-data" action="receive\_file\_post.php" method="post"> 您的大名: <input type=text name=user><br> <input type="hidden" name="MAX\_FILE\_SIZE" value="30000">  <!--最大取值2147483647--> 上传文件: <input name="userfile" type="file"><br><br> <input type="submit" value="开始上传"> </form>** 其中，

1.  请注意<form enctype="multipart/form-data"......>这是一个标签，我们要实现文件的上传，必须指定为multipart/form-data，否则服务器将不知道要干什么。
2.  值得注意的是文件upload\_file\_post.php中表单选项 MAX\_FILE\_SIZE 的隐藏值域，通过设置其Value(值)可以限制上载文件的大小。
3.  MAX\_FILE\_SIZE 的值只是对浏览器的一个建议，实际上它可以被简单的绕过。因此不要把对浏览器的限制寄希望于该值。实际上，PHP 设置中的上传文件最大值，是不会失效的。但是最好还是在表单中加上 MAX\_FILE\_SIZE，因为它可以避免用户在花时间等待上传大文件之后才发现该文件太大了的麻烦。

**<!--使用POST上传文件示例：recieve\_file\_post.php----------------------------> <?php uploaddir=′./uploadfiles/′;if(!moveuploadedfile(\_FILES\['userfile'\]\['tmp\_name'\],uploaddir._FILES\['userfile'\]\['name'\])) echo "文件上传失败，错误信息：".FILES\[′userfile′\]\[′error′\]."<br>";elseecho"文件"._FILES\['userfile'\]\['name'\]."上传成功<br>"; ?>** 以上范例中 $_FILES 数组的内容如下所示。我们假设文件上传字段的名称为 userfile（名称可随意命名）

*   $_FILES\['userfile'\]\['name'\] 客户端机器文件的原名称。
*   $_FILES\['userfile'\]\['type'\] 文件的 MIME 类型，需要浏览器提供该信息的支持，例如“image/gif”。
*   $_FILES\['userfile'\]\['size'\] 已上传文件的大小，单位为字节。
*   $\_FILES\['userfile'\]\['tmp\_name'\] 文件被上传后在服务端储存的临时文件名。
*   $_FILES\['userfile'\]\['error'\] 和该文件上传相关的错误代码

如果名为file1.doc和file2.doc文件被上传，则FILES\[′userfile′\]\[′name′\]\[0\]将包含文件file1.doc的名称，而FILES\[′userfile′\]\[′name′\]\[0\]将包含文件file1.doc的名称，而_FILES\['userfile'\]\['name'\] \[1\]则将包含文件file.doc的名称。

1.  **值：0; 没有错误发生，文件上传成功。**
2.  **值：1; 上传的文件超过了 php.ini 中 upload\_max\_filesize 选项限制的值。**
3.  **值：2; 上传文件的大小超过了 HTML 表单中 MAX\_FILE\_SIZE 选项指定的值。**
4.  **值：3; 文件只有部分被上传。**
5.  **值：4; 没有文件被上传。**

我上传的一首MP3，大概4M多，我看错误代码是2，开来是我的HTML 表单中 MAX\_FILE\_SIZE 选项指定的值太小了，我看了一下，数值是30000，我又查了一下，这个设置的单位是字节，看来的确是这个问题了，把值设置大点不就OK了吗，我一下改为 了10M，看来是没问题了。然后进行测试，可又出现了错误代码1。哎！怎么还有问题啊。不过没关系，一步步来吗。 不就是错误代码1吗，哦，原来是upload\_max\_filesize限制值太小了，二话不说，改为10M了。哈哈。。。。。。测试，晕，还是不行。我就继续找php.ini设置的资料。看到下面的东西： **PHP上传文件涉及到的参数**PHP默认的上传限定是最大2M，想上传超过此设定的文件，需要调整PHP、apache等的一些参数. 下面，我们简要介绍一下PHP文件上传涉及到的一些参数：

*   **file_uploads**

是否允许通过HTTP上传文件的开关，默认为ON即是开

*   **upload\_tmp\_dir**

upload\_tmp\_dir用来说明PHP上传的文件放置的临时目录，要想上传文件，得保证服务器没有关闭临时文件和有对文件夹的写权限，如果未指定则PHP使用系统默认值

*   **upload\_max\_filesize**

允许上传文件大小的最大值，默认为2M

*   **post\_max\_size**

控制在采用POST方法进行一次表单提交中PHP所能够接收的最大数据量。如果希望使用PHP文件上传功能，则需要将此值改为比upload\_max\_filesize要大

*   **max\_input\_time**

以秒为单位对通过POST、GET以及PUT方式接收数据时间进行限制。如果应用程序所运行环境处在低速链路上，则需要增加此值以适应接收数据所需的更多时间

*   **memory_limit**

为了避免正在运行的脚本大量使用系统可用内存，PHP允许定义内存使用限额。通过memory\_limit变量来指定单个脚本程序可以使用的最大内存容量变量memory\_limit的值应当适当大于post\_max\_size的值

*   **max\_execution\_time**

max\_execution\_time 设置了在强制终止脚本前PHP等待脚本执行完毕的时间，此时间以秒计算。当脚本进入了一个无限循环状态时此变量非常有用。然而，当存在一个需要很长时间完 成的合法活动时（例如上传大型文件），这项功能也会导致操作失败。在这样的情况下必须考虑将此变量值增加，以避免PHP在脚本正在执行某些重要过程的时候 将脚本关闭

*   对于**linux**主机，可能在**/etc/httpd/conf.d/access.conf/**下面里面还有**php.conf** 文件，这个文件可能会解决一些系统的文件大小限制问题

我就照着上边的，把限制都改得超大，这回应该没有问题了吧，都设置好了。测试一下喽。真郁闷，还是提示错误代码1。不对啊，我设置的都很大啊，不会有问题的。怎么回事呢。 算了，呆会再研究，先让同学玩吧，去买饭了，不然呆会餐厅没饭了，呵呵。。肚子饿了！ 回来了，继续研究那个烦人的问题。我上传个小文件吗。上传个WORD文档，才两百多K，哦耶！成功一次。弄个1M多的压缩包，又成功了，再试试我那歌曲 了。哎！还是不成功。看了看那首歌有5M多，上传个小店的歌曲了。我找了个2M多的歌曲上传，还是不成功。再试个不到2M的歌吧，居然成功了。看来是不能 上传大于2M的东西了。奇怪啊，不大对啊，我设置的限制是10M 啊，远远大于了。难道是我设置没成功。我又看了看设置，没有问题的。 。。。。。。。。。。。。 我不停的想啊，累死了，2M........这不就是php.ini设置上传限制的默认值吗，我改了怎么没有成功呢。哦？？可能是服务器得重启一下，以前 也经常遇到非重启服务器才能解决问题的情况。于是我就重启的Apache（我用的是这个），再试试了。成功了！！这次真的是搞定了。 以前在配置PHP环境的时候，也遇到过类似的情况，感觉配置的环境没有问题，可就是测试不成功，一般都是需要重启Apache等服务器了。所以呢，以后，已更改类似php.ini等文件后，一定要记得重启服务器。 转自：[http://dxnumber.blog.163.com/blog/static/173757526201331994835335/](http://www.cnblogs.com/c-961900940/p/4059519.html)