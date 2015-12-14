---
layout: post
title:  "Egit Patch"
excerpt: "Git为我们提供了Patch功能，Patch中包含了源码更改的描述，能够应用于其他Eclipse工作空间或者Git仓库。"
date:   2015-11-13 14:16:58 +0800
categories: Egit
tags: [Egit, Eclipse]
---
---

Git为我们提供了Patch功能，Patch中包含了源码更改的描述，能够应用于其他Eclipse工作空间或者Git仓库。也就是说，可以将当前提交导出至其他分支或者项目中。

举个例子，项目A、B中使用了相同的JSP代码：ShowHello.jsp，当在A项目中修改了ShowHello.jsp，那么需要将这个修改复制到B项目，如果只是一个文件修改还好说，如果是多个目录下多个文件的修改就麻烦了。这是时候我们就可以用Patch，将A项目的修改同步到B项目。

下面说一下操作流程。

1  A项目中修改完成后，进行提交(commit)和上传(push)，在历史中(项目右击→Team→Show In History)可以看到本次提交与提交的文件：

![截图]({{ site.url }}/img/egit patch/1.png)

2  图中下方方框中的三个文件就是我们修改的文件，上方方框中为我们的提交，右击选择Creat Patch…：

![截图]({{ site.url }}/img/egit patch/2.png)

3  弹出如下窗口，在窗口中选择存储位置和文件名，默认文件名为此次commit的内容：

![截图]({{ site.url }}/img/egit patch/3.png)

4  点击Next，到一下个页面：

![截图]({{ site.url }}/img/egit patch/4.png)

5  按默认就可以，点击Finnish。此时在你指定的位置就生成了Patch文件。此时在项目B上右击选择Team→Apply Patch…,在弹出界面上选择刚刚生成的Patch文件，点击Next：

![截图]({{ site.url }}/img/egit patch/5.png)

6  选择要打Patch的项目，点击Next：

![截图]({{ site.url }}/img/egit patch/6.png)

7  重点来了，如果是是不同的项目在Patch options的Ignore leading path name segments这里要选成1（默认为0），选完之后下面框的图标中出现蓝色的箭头，双击每个文件都可以看到文本对比（Text Compare），可以看看代码是不是自己要的。最后Commit and push就可以了。

![截图]({{ site.url }}/img/egit patch/7.png)


相对于Git，Egit提供的功能还是比较少的，但是够用。如果想对git的Patch有深入的了解，请移步[老Z的博客-Git的Patch功能](http://www.cnblogs.com/y041039/articles/2411600.html)。

如果在Apply Patch时中文变为乱码，则需要将生产的Patch文件用记事本打开另存为编码方式为ANSI的文件，然后再Apply Patch。
