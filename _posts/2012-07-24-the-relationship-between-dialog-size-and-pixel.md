---
layout: post
title:  "对话框大小与像素关系"
excerpt: "对话框大小与像素关系."
date:   2012-07-24 22:30:12 +0800
categories: MFC
tags: [MFC]
comments: true
---
---

我们知道可以用记事本打开.rc文件，然后改里面的坐标，来改变对话框大小，如：
以下是rc文件

{% highlight text %}
/////////////////////////////////////////////////////////////////////////////
//
// Dialog
//

IDD_ABOUTBOX DIALOGEX 0, 0, 170, 62
STYLE DS_SETFONT | DS_MODALFRAME | DS_FIXEDSYS | WS_POPUP | WS_CAPTION | WS_SYSMENU
CAPTION "关于 Server"
FONT 9, "MS Shell Dlg", 0, 0, 0x1
BEGIN
    ICON            IDR_MAINFRAME,IDC_STATIC,14,14,21,20
    LTEXT           "Server，1.0 版",IDC_STATIC,42,14,114,8,SS_NOPREFIX
    LTEXT           "Copyright (C) 2010",IDC_STATIC,42,26,114,8
    DEFPUSHBUTTON   "确定",IDOK,113,41,50,14,WS_GROUP
END
{% endhighlight %}

只要把`IDD_ABOUTBOX DIALOGEX 0, 0, 170, 62`最后两个数改一下就可以改变about窗口的大小。

对话框资源中的尺寸数值是对话框单位，该大小的单位不是像素而是DLU（dialog logical units），它是与分辨率无关的坐标单位。它与像素之间的转换关系与当前对话框字体有关。不是像素，要转换成像素，可以借助于 MapDialogRect 来转换。
如果想手动计算，用下面的算法：

{% highlight text %}
  pixelX = MulDiv(dialogX, 对话框水平基本单位, 4)
  pixelY = MulDiv(dialogY, 对话框垂直基本单位, 8)
{% endhighlight %}

DialogLayout类是一个简单的布置管理器，用来配合Win32 API中的对话框逻辑单位(dialog logical units = DLU)工作。对话框逻辑单位是与分辨率无关的坐标单位，它对于对话框中控制部件的布置很有作用。从DLU到象素有一个映射，此映射是基于对话框所用的字体的。DLU的一个X方向的坐标单位相当于对话框中所用字体的平均宽度的1/4，Y方向的坐标单位相当于对话框对话框所用字体高度的1/8。注意字体平均宽度的计算并非是所有字符的平均，而是字母a…z（包括大写）的宽度的平均，换句话说，它等于字符串”a…zA…Z”的长度除以52。

使用Visual Studio 6.0(Visual C++ 6.0)开发的过程中，对话框中的控件在资源编辑器中的尺寸和其实际的像素尺寸之间的对应问题非常的令人烦恼。特别是在要求对话框控件大小随屏幕分辨率或程序窗口大小变化而变化时就更加令人挠头。

原因就在于，资源编辑器中的单位（DLU）与屏幕像素之间的对应关系随着对话框字体种类和大小的变化而变化。

（1）在水平方向1 DLU == 1/4 字体平均宽度；

（2）在垂直方向1 DLU == 1/8 字体平均高度。

 这一对应关系由于所使用字体的多变而难以确定。在绝大多数情况下，通过上面公式所计算的DLU甚至不会是整数像素。
为了在资源编辑器编辑的过程中就比较好的把握做出来的控件在屏幕上的像素尺寸，根据（1），思路：在对话框资源编辑器中应该采用等宽字体；根据（2），思路：最好采用所谓“系统”字体，这样字体高度也是固定的。

验证一下：在对话框资源编辑器中打开“Dialog Properties”，单击“Font...”按钮，为对话框选择字体。考察“FixedSys”和“System”两种，首先，从网上搜索得知，它们是等宽字体；其次，这两种字体只有一种尺寸大小“12”，这说明字体高度是固定的。

实地测试一下，在VC对话框工程中，将对话框的字体改为“FixedSys”或“System”，字号大小改为“12（即小四）”，并在对话框中创建一个100*100 DLU的按钮。在按钮单击响应函数里，用GetWindowRect()或GetClientRect()取得按钮尺寸。设置断点调试观察结果：按钮的像素尺寸是200*200！这表明对话框资源编辑器中的1 DLU现在等于2 Pixels。这样对于我们的设计就方便很多了。

如果屏幕分辨率改变了，结果如何呢？在不同的显示器上进行测试，结果都一样，仍然是1 DLU == 2 Pixels。

还有没有别的字体有这样的效果呢？“Terminal”字体也可以，选择字号为12，测试结果也是水平方向/垂直方向1 DLU == 2 Pixels。不过有个毛病：选择了该字体的对话框在资源编辑器里看起来怪怪的，水平方向1 DLU和垂直方向1 DLU的长度不同，好像被压扁了一样。但程序运行起来则没问题。另外，选择不同的“Terminal”字体大小，则对应关系也会改变。

到这里，索性对其他几种常用的字体也测试了一下，发现Verdana和宋体效果比较好（虽然对于英文来说这两种都不是等宽字体。而对于汉字，一般使用的汉字字体都是等宽的，方块字嘛）。下面是测试结果（仍然用100*100的按钮来测试）：

{% highlight text %}
字体     / 字号 / 水平尺寸 / 垂直尺寸
Verdana / 8   / 175     / 163
        / 9   / 200     / 175
        / 10  / 200     / 200
        / 11  / 225     / 225
        / 12  / 250     / 225
宋体     / 8   / 150     / 138
        / 9   / 150     / 150
        / 10  / 175     / 163
        / 11  / 200     / 188
        / 12  / 200     / 200
{% endhighlight %}

结论1：如果对FixedSys和System字体的效果不满意，选用12号宋体/10号Verdana是比较好的

结论2：虽然只能使用若干种有限的字体，但能给编程带来一些方便，还是值得的（相比字体效果的损失）
