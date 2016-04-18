---
layout: post
title:  "Eclipse统计代码行数"
excerpt: "在Eclipse中统计代码行数。"
date:   2015-11-07 15:53:29 +0800
categories: Eclipse
tags: [Eclipse]
comments: true
---
---

如何统计项目的代码行数呢?其实使用Eclipse进行统计很方便.

1  点击要进行统计代码行数的的项目或者文件夹，在菜单栏点击**Search**，然后点击**File...** ,当然也可以直接使用快捷键**Ctrl+H**

![截图]({{ site.url }}/img/count-the-line-numbers-in-eclipse/1.png)

2  选中正则表达式(Regular expression)，如果统计所有行数，输入`\n`；如果搜索非空行行数，输入`\s*\n`，如果搜索空行行数，输入`^\s*\n`

3  如果统计选定范围的所有文件行数，在File name patterns 中输入*，如果统计java则输入*.java ，如果统计java、jsp、xml则输入`*.java, *.jsp, *.xml`

4  在范围（Scope）里选中Selected resources。

5  在Search窗口就会显示出项目或文件的代码行数。
