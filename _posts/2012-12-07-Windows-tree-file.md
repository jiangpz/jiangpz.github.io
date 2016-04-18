---
layout: post
title:  "Windows下生成树状目录结构的方法"
excerpt: "Windows下生成树状目录结构的方法."
date:   2012-12-07 15:30:12 +0800
categories: Windows
tags: [Windows]
comments: true
---
---

命令格式：

以图形显示驱动器或路径的文件夹结构。

{% highlight bat linenos %}
TREE [drive:][path] [/F] [/A]

   /F   显示每个文件夹中文件的名称。
   /A   使用 ASCII 字符，而不使用扩展字符。
{% endhighlight %}

例子：

{% highlight bat linenos %}
tree /F D:\Study > D:\tree.txt
{% endhighlight %}

就是将`D:\Study`这个文件夹的目录结构以树状形式输出报告到文件`D:\tree.txt`中。
