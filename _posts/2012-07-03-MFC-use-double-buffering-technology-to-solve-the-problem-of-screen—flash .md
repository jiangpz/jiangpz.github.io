---
layout: post
title:  "MFC双缓冲技术解决屏闪问题"
excerpt: "传统的绘图方式实际上是一种单缓冲,相邻两帧图像之间存在的巨大差异会造成屏闪问题."
date:   2012-07-03 22:30:12 +0800
categories: MFC
tags: [MFC, C]
---
---

#### 屏幕闪烁的根本原因：

相邻两帧图像之间存在的巨大差异造成的，而windows gdi的图形刷新方式使得任何两帧图像之间都存在着巨大的差异，因为windows gdi在进行刷新之前都会首先将整个屏幕刷成白色，就相当于在电影胶片的相邻两帧之间都插入了一个白色的帧，这也就是为什么屏幕闪烁时总是看到一个隐约的白色窗口在闪烁而不是一个红色的窗口在闪烁。双缓冲图形刷新技术避免了windows gdi刷新的问题，其没有在连续的两帧之间插入白色的帧，从而解决了屏幕闪烁的问题。

#### 双缓冲图形刷新技术的原理

双缓冲图形刷新技术顾名思义是采用双缓存实现的。传统的绘图方式实际上是一种单缓冲。在windows中每一种设备都在内存中有一个设备描述表与其对应，这个设备描述表实际上就是一个内存缓冲区。传统的绘图中我们是将图形绘制在设备描述表缓冲区中，然后由gdi自动的将设备描述表中的图像拷贝到显存中进行显示。这样一个自动的拷贝过程屏蔽了传统的绘图方式是单缓冲的实质，使我们感觉到我们是在直接操纵显存一样。双缓冲图形刷新技术在内存中有两片缓存，除了设备描述表以外还有一个需要手动建立的与设备描述表缓冲区（前端缓冲区）相兼容的后备缓冲区。绘图过程中，首先将图形绘制在后备缓冲区中，然后在手动的将后备缓冲区中的图像拷贝到前端缓冲区中，再由gdi自动将前端缓冲区中的图像拷贝到显存完成图形的显示过程。

#### 示例代码

1、首先在OnDraw()或者OnPaint()中添加下列代码

{% highlight c linenos %}
 //定义一个位图对象
 CBitmap  bitmap，MemBitmap;

 CDC MemDC;

 bitmap.LoadBitmap(IDB_BITMAP3);
 BITMAP bmp;
 bitmap.GetBitmap(&bmp);
 //建立与屏幕设备描述表（前端缓冲区）兼容的内存设备描述表句柄（后备缓冲区）
 MemDC.CreateCompatibleDC(NULL);
 //这时还不能绘图，因为没有位图的设备描述表是不能绘图的
 //下面建立一个与屏幕设备描述表（或者内存设备描述表）兼容的位图
 MemBitmap.CreateCompatibleBitmap(pDC,600,660);
 //将位图选入到内存设备描述表
 //只有选入了位图的设备描述表才有地方绘图，画到指定的位图上
 CBitmap *pOldBit=MemDC.SelectObject(&MemBitmap);

 MemDC.CreateCompatibleDC(pDC);
 MemDC.SelectObject(&bitmap);
 MemDC.MoveTo(。。。);
 MemDC.LineTo(。。。);
 pDC->BitBlt(0,0,nWidth,nHeight,&MemDC,0,0,SRCCOPY);

 //绘图完成后的清理
 MemBitmap.DeleteObject();
 MemDC.DeleteDC();
{% endhighlight %}

2、添加WM_ERASEBKGND响应函数，并清除响应函数的生成代码在其中添加如下代码

{% highlight c linenos %}
BOOL OnEraseBkgnd(CDC* pDC)
{
    // TODO: 在此添加消息处理程序代码和/或调用默认值
    //return CDialog::OnEraseBkgnd(pDC);
    return FALSE;
}
{% endhighlight %}
