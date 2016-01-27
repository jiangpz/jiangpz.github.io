---
layout: post
title:  使用vmware提示无法打开内核设备 \\.\Global\vmx86: 系统找不到指定的文件
excerpt: 使用vmware提示无法打开内核设备 \\.\Global\vmx86: 系统找不到指定的文件。
date:   2016-01-27 09:46:21 +0800
categories: Vmware
tags: [Vmware]
---

问题描述：vmware启动提示“无法打开内核设备 \\.\Global\vmx86: 系统找不到指定的文件”

这是因为虚拟机服务没有开启:

点击“开始→运行”，在运行框中输入 CMD  回车打开命令提示符，然后依次执行以下命令。

{% highlight sh %}
net start vmci
net start vmx86
net start VMnetuserif
sc config vmci=auto
sc config vmx86=auto
sc config VMnetuserif=auto
{% endhighlight %}
