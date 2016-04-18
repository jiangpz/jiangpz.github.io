---
layout: post
title:  "Linux下is not in the sudoers file解决方法"
excerpt: "Linux下使用sudo时报is not in the sudoers file解决方法。"
date:   2016-03-5 10:46:25 +0800
categories: Linux
tags: [Linux]
comments: true
---

当我们使用`sudo`命令切换用户的时候可能会遇到提示以下错误：

{% highlight text %}
xxx is not in the sudoers file. This incident will be reported.
{% endhighlight %}

其中xxx是你当前的用户名，究其原因是用户没有加入到sudo的配置文件里.

切换到root用户，运行`visudo`命令

{% highlight sh %}
[gordon@localhost Workspace]$ su
Password:
[root@localhost Workspace]# visudo
{% endhighlight %}

在打开的配置文件中，找到`root ALL=(ALL) ALL`，在下面添加一行
`xxx ALL=(ALL) ALL `,其中xxx是你要加入的用户名称,在vi下可以用"/root"来查找

{% highlight sh %}
## Next comes the main part: which users can run what software on
## which machines (the sudoers file can be shared between multiple
## systems).
## Syntax:
##
##      user    MACHINE=COMMANDS
##
## The COMMANDS section may have other options added to it.
##
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
gordon  ALL=(ALL)       ALL
{% endhighlight %}

输入`:wq`保存并退出配置文件，再次使用`sudo`命令就不会有上面的提示了。
