---
layout: post
title:  "Linux 开放80、8080端口或者开放某个端口"
excerpt: "Linux 开放80、8080端口或者开放某个端口。"
date:   2016-03-16 14:26:08 +0800
categories: Linux
tags: [Linux]
---

在安装CentOS时只开启了22端口，在Linux上部署项目之后，其他机器不能访问网站。

我们可以通过超级管理员使用`iptables -L in`命令查看当前端口开放情况：

{% highlight sh %}
[root@localhost gordon]# iptables -L -n
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED
ACCEPT     icmp --  0.0.0.0/0            0.0.0.0/0           
ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22
REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
{% endhighlight %}

现在只开启了22端口.Linux防火墙中默认是关闭8080端口的。

可以用两种方式解决问题，一个是关闭防火墙，另一个就是让防火墙开放这个端口。

关闭防火墙命令:`service iptables stop` (不推荐)

开放8080端口的解决步骤如下：

1、修改`/etc/sysconfig/iptables` 文件，增加如下一行：
{% highlight sh %}
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
{% endhighlight %}
如果已经打开22端口，可以直接复制22端口的那一行然后将22改为8080。
重启iptables：`service iptables restart`

2、重启防火墙，这里有两种方式重启防火墙

a) 重启后生效
	开启： `chkconfig iptables on`
	关闭：` chkconfig iptables off`

b) 即时生效，重启后失效
	开启： service iptables start
  关闭： service iptables stop

开放一个范围的端口3000到5000

{% highlight sh %}
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 3000:5000 -j ACCEPT
{% endhighlight %}
