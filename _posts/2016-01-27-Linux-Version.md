---
layout: post
title:  "查看linux内核版本号版本信息"
excerpt: "查看linux版本。"
date:   2016-01-27 10:00:21 +0800
categories: Linux
tags: [Linux]
comments: true
---

####查看linux内核版本号

第一种：登录linux，在终端输入 `cat /proc/version`

{% highlight sh %}
[root@localhost ~]# cat /proc/version
Linux version 2.6.32-431.el6.x86_64 (mockbuild@nkkojibuilder5) (gcc version 4.4.7 20120313 (NeoKylin 4.4.7-4) (GCC) ) #1 SMP Fri Mar 28 08:38:24 CST 2014
{% endhighlight %}

第二种：登录linux，在终端输入 `uname -a`，可列出linux的内核版所有信息：

{% highlight sh %}
[root@localhost ~]# uname -a
Linux localhost.localdomain 2.6.32-431.el6.x86_64 #1 SMP Fri Mar 28 08:38:24 CST 2014 x86_64 x86_64 x86_64 GNU/Linux
{% endhighlight %}

第三种：在Linux终端输入 `unmae -r`，可查看linux的内核版本号

{% highlight sh %}
[root@localhost ~]# uname -r
2.6.32-431.el6.x86_64
{% endhighlight %}

####查看linux版本信息

第一种：登录到linux服务器执行 `lsb_release -a` 命令，即可查看所有版本信息，如下图：

{% highlight sh %}
[root@localhost ~]# lsb_release -a
LSB Version:    :base-4.1-amd64:base-4.1-noarch:core-4.1-amd64:core-4.1-noarch:graphics-4.1-amd64:graphics-4.1-noarch:printing-4.1-amd64:printing-4.1-noarch
Distributor ID: NeoKylinAdvancedServer
Description:    NeoKylin Linux Advanced Server release 6.5 (Beryllium)
Release:        6.5
Codename:       Beryllium
{% endhighlight %}

第二种：登录到linux执行 `cat /etc/issue`

{% highlight sh %}
[root@localhost ~]# cat /etc/issue
NeoKylin Linux Advanced Server release 6.5 (Beryllium)
Kernel \r on an \m
{% endhighlight %}
