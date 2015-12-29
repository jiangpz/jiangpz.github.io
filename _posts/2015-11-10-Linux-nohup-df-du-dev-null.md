---
layout: post
title:  "Linux命令：nohup、df、du与/dev/null"
excerpt: "Linux命令：nohup、df、du与/dev/null的使用方式"
date:   2015-11-10 09:53:29 +0800
categories: Linux
tags: [Linux]
---
---

早上开始工作时发现服务器挂掉了，重启TongWeb时有报错：

![截图]({{ site.url }}/img/Linux-nohup-df-du-dev-null/1.png)

上面的红框圈错了，第一个红框的下一行：

{% highlight sh %}
java.io.IOException: No Space left on device
{% endhighlight %}

我们用`df`查看发现磁盘没有空间了。

##### df和du

首先我们了解df和du命令。

- df可以查看一级文件夹大小、使用比例、档案系统及其挂入点，但对文件却无能为力。
- du可以查看文件及文件夹的大小。

两者配合使用，非常有效。比如用df查看哪个一级目录过大，然后用df查看文件夹或文件的大小，如此便可迅速确定症结。

###### df命令

df命令可以显示目前所有文件系统的可用空间及使用情形，上图中我们执行了`df -h`，参数`-h`表示使用「Human-readable」的输出，也就是在档案系统大小使用 GB、MB 等易读的格式。

上面的命令输出的第一个字段（Filesystem）及最后一个字段（Mounted on）分别是档案系统及其挂入点。我们可以看到 /dev/sda1 这个分割区被挂在根目录下。

接下来的四个字段 Size、Used、Avail、及 Use% 分别是该分割区的容量、已使用的大小、剩下的大小、及使用的百分比。 FreeBSD下，当硬盘容量已满时，您可能会看到已使用的百分比超过100%，因为FreeBSD会留一些空间给root，让root在档案系统满时，还是可以写东西到该档案系统中，以进行管理。

###### du命令

du命令用于查询文件或文件夹的磁盘使用空间。

如果当前目录下文件和文件夹很多，使用不带参数du的命令，可以循环列出所有文件和文件夹所使用的空间。这对查看究竟是那个地方过大是不利的，所以得指定深入目录的层数，参数：`--max-depth=`，这是个极为有用的参数！注意使用“\*”，可以得到文件的使用空间大小.

![截图]({{ site.url }}/img/Linux-nohup-df-du-dev-null/2.png)

![截图]({{ site.url }}/img/Linux-nohup-df-du-dev-null/3.png)

提醒：一向命令比linux复杂的FreeBSD，它的du命令指定深入目录的层数却是比linux简化，为 -d。

现在我们就能够确定问题出在nohup.out这个文件上。现场删除这个文件后，发现：

![截图]({{ site.url }}/img/Linux-nohup-df-du-dev-null/4.png)

文件还在，在/home/.Trash-0里面又发现这个文件，说明，文件被移动到回收站中（如果是CentOS，这个路径应该是/home/用户名/.local/share/Trash/files），可能删除是在可视化界面中删除的，那么在.Trash-0中用rm删除就行了。

##### nohup命令

###### nohup简介

用途：不挂断地运行命令。

语法：nohup Command [ Arg … ] [　& ]

描述：nohup 命令运行由 Command 参数和任何相关的 Arg 参数指定的命令，忽略所有挂断（SIGHUP）信号。在注销后使用 nohup 命令运行后台中的程序。要运行后台中的 nohup 命令，添加 & （ 表示”and”的符号）到命令的尾部。

无论是否将 nohup 命令的输出重定向到终端，输出都将附加到当前目录的 nohup.out 文件中。如果当前目录的 nohup.out 文件不可写，输出重定向到 $HOME/nohup.out 文件中。如果没有文件能创建或打开以用于追加，那么 Command 参数指定的命令不可调用。如果标准错误是一个终端，那么把指定的命令写给标准错误的所有输出作为标准输出重定向到相同的文件描述符。

退出状态：该命令返回下列出口值：

- 126 可以查找但不能调用 Command 参数指定的命令。
- 127 nohup 命令发生错误或不能查找由 Command 参数指定的命令。

否则，nohup 命令的退出状态是 Command 参数指定命令的退出状态。

###### nohup命令及其输出文件

nohup命令：如果你正在运行一个进程，而且你觉得在退出帐户时该进程还不会结束，那么可以使用nohup命令。该命令可以在你退出帐户/关闭终端之后继续运行相应的进程。nohup就是不挂断的意思( no hang up)。

该命令的一般形式为：nohup command &

###### 使用nohup命令提交作业
如果使用nohup命令提交作业，那么在缺省情况下该作业的所有输出都被重定向到一个名为nohup.out的文件中，除非另外指定了输出文件：

{% highlight sh %}
nohup command > myout.file 2>&1 &
{% endhighlight %}

在上面的例子中:

- 0: stdin (standard input)
- 1: stdout (standard output)
- 2: stderr (standard error) ；2>&1是将标准错误（2）重定向到标准输出（&1），标准输出（&1）再被重定向输入到myout.file文件中。

在当shell中提示了nohup成功后还需要按终端上键盘任意键退回到shell输入命令窗口，然后通过在shell中输入exit来退出终端；如果在nohup执行成功后直接点关闭程序按钮关闭终端，进程会自动被关闭，察看nohup.out可以看到在关闭终端瞬间服务自动关闭。所以这时候会断掉该命令所对应的session，导致nohup对应的进程被通知需要一起shutdown。

但是此时还是会产生nohup文件的，需要执行：

{% highlight sh %}
nohup ./xxxxxx & > /dev/null
{% endhighlight %}

“&”之后要有空格，不然就变成了linux重定向中&>，它和>&是一个意思，是“复制一个文件描述符”的意思，nohup就会找不到结束符号。

###### /dev/null

shell中可能经常能看到：`echo log > /dev/null 2>&1`，命令的结果可以通过%>的形式来定义输出：

- /dev/null ：代表空设备文件
- \>  ：代表重定向到哪里，例如：echo "123" > /home/123.txt
- 1  ：表示stdout标准输出，系统默认值是1，所以">/dev/null"等同于"1>/dev/null"
- 2  ：表示stderr标准错误
- &  ：表示等同于的意思，2>&1，表示2的输出重定向等同于1

`1 > /dev/null 2>&1` 语句含义：

- 1 > /dev/null ： 首先表示标准输出重定向到空设备文件，也就是不输出任何信息到终端，说白了就是不显示任何信息。
- 2>&1 ：接着，标准错误输出重定向（等同于）标准输出，因为之前标准输出已经重定向到了空设备文件，所以标准错误输出也重定向到空设备文件。

实例解析：

cmd >a 2>a 和 cmd >a 2>&1 为什么不同？

- cmd >a 2>a ：stdout和stderr都直接送往文件 a ，a文件会被打开两遍，由此导致stdout和stderr互相覆盖。
- cmd >a 2>&1 ：stdout直接送往文件a ，stderr是继承了FD1的管道之后，再被送往文件a 。a文件只被打开一遍，就是FD1将其打开。

两者的不同点在于：

- cmd >a 2>a 相当于使用了FD1、FD2两个互相竞争使用文件 a 的管道；
- cmd >a 2>&1 只使用了一个管道FD1，但已经包括了stdout和stderr。

从IO效率上来讲，cmd >a 2>&1的效率更高。
