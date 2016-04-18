---
layout: post
title:  "一个对话框，初始时没有OnInitDialog()函数，我们如何初始化其数据成员及函数"
excerpt: "一个对话框，初始时没有OnInitDialog()函数，我们如何初始化其数据成员及函数."
date:   2012-07-25 22:30:12 +0800
categories: MFC
tags: [MFC]
comments: true
---
---

在vc对话框的操作中，很多资料上都讲到可以使用虚函数OnInitDialog()对其进行初始化。

但是在类的添加虚函数的列表中，并没有这个函数。这是怎么回事呢？

事实上，在消息框里面有一个 WM_INITDIALOG 消息，添加这个消息，则自动添加了一个OnInitDialog()函数。

这样就可以对对画框进行初始化了。

首先，按ctrl + W，打开一对话框，找到在添加OnInitDialog()函数的对话框。找到WM_INITDIALOG 消息，添加。即可。

如果在是VC2005中，不可以通过`ctrl+w`打开对话框添加。此时，我们可以在资源管理器中选中要添加的对话框，然后在最右边的属性对话框中找到一个“重写”按钮，在这个按钮下，可以找到OnInitDialog这个函数，选中，并点击添加，OK！

在VC2008中，在类视图中，找到要添加OnInitDialog()函数的类，右击->属性，在属性对话框中，有个绿色 的小立方体，也就是“重写”，点击它，在“通用”里面就有OnInitDialog；点击右侧的下拉菜单，就可以添加OnInitDialog()函。
