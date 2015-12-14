---
layout: post
title:  "Windows某个端口被占用情况"
excerpt: "安装完CentOS 6.6系统之后，我们需要设置系统自带的中文输入法."
date:   2013-01-09 19:00:42 +0800
categories: cmd
tags: [cmd, Windows]
---
---

在启动Jekyll时经常遇到下面这个报错：

{% highlight bat linenos %}
Configuration file: D:/STSWorkspace/jiangpz.github.io/_config.yml
            Source: D:/STSWorkspace/jiangpz.github.io
       Destination: D:/STSWorkspace/jiangpz.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 2.243 seconds.
 Auto-regeneration: enabled for 'D:/STSWorkspace/jiangpz.github.io'
Configuration file: D:/STSWorkspace/jiangpz.github.io/_config.yml
jekyll 3.0.1 | Error:  Permission denied - bind(2) for 127.0.0.1:4000
{% endhighlight %}

最后一行的报错一般情况是端口4000被占用，现在记录一下解决这个问题的方法。

1  开始→运行→bat，或者是`window+R`组合键，调出命令窗口,也可以使用[Cmder](http://www.softpedia.com/get/Programming/Other-Programming-Files/Cmder.shtml)。

2  输入命令：`netstat -ano`，可以列出所有端口的情况。可以在列表中看到端口使用情况，这个列表一般很长，如果要查找某个端口，可以使用`netstat -aon|findstr "XXXX"`，例如我们查看4000端口占用情况，则使用`netstat -aon|findstr "4000"`，结果如下：

{% highlight bat %}
协议    本地地址                外部地址                状态             PID
TCP    127.0.0.1:4000         0.0.0.0:0              LISTENING       884
TCP    127.0.0.1:4000         127.0.0.1:58330        ESTABLISHED     884
TCP    127.0.0.1:58330        127.0.0.1:4000         ESTABLISHED     5740
{% endhighlight %}

其中第一行是没有的，这里写上是为了方便查看PID。可以确定占用端口的程序PID为“884”。

3  继续输入`tasklist|findstr "884"`，回车，查看PID为“884”的是哪个进程或者程序，他占用了4000端口。

{% highlight bat lineos %}
映像名称                       PID 会话名              会话#       内存使用
========================= ======== ================ =========== ============
vmnetdhcp.exe                 3076 Services                   0     10,884 K
igfxpers.exe                  3536 Console                    1     16,884 K
FoxitProtect.exe               884 Services                   0     11,596 K
Proxifier.exe                 6884 Console                    1     36,748 K
BaofengPlatform.exe           8840 Console                    1     20,004 K
{% endhighlight %}

4  发现是"FoxitProtect.exe"这个程序占用了端口，使用`taskkill /f /t /im FoxitProtect.exe`结束他。

用到的命令如下：
{% highlight bat lineos %}
netstat -aon|findstr "XXXXX"
tasklist|findstr "XXXXX"
taskkill /f /t /im XXXXX.exe
{% endhighlight %}
