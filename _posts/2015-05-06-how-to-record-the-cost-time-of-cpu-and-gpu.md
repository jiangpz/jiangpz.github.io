---
layout: post
title:  "CUDA中记录GPU耗时与C编程中记录CPU耗时的方法"
excerpt: "CUDA中记录GPU耗时与C编程中记录CPU耗时的方法"
date:   2013-05-06 09:55:00 +0800
categories: CUDA
tags: [CUDA, C++]
comments: true
---
---

CUDA中记录GPU耗时的方法参考《CUDA By Example》中介绍的方法；在GPU端代码的开始与结束的部分分别增加：

{% highlight cuda linenos %}
// capture the start time
cudaEvent_t     start, stop;
cudaEventCreate( &start );
cudaEventCreate( &stop );
cudaEventRecord( start, 0 );
{% endhighlight %}

和

{% highlight cuda linenos %}
// get stop time, and display the timing results
cudaEventRecord( stop, 0 );
cudaEventSynchronize( stop );
float   elapsedTime;
cudaEventElapsedTime( &elapsedTime,
start, stop );
printf( "Time to generate:  %3.1f ms\n", elapsedTime );

cudaEventDestroy( start );
cudaEventDestroy( stop );
{% endhighlight %}

C编程中记录CPU耗时的方法参考论坛中的一个帖子[http://club.topsage.com/thread-2644760-1-1.html](http://club.topsage.com/thread-2644760-1-1.html)：

{% highlight cpp linenos %}
//Compile_Environment:Microsoft Visual C++2010
#include stdio.h
#include Windows.h   //该头文件不能少，且需在Winbase.h前
#include  Winbase.h   //该头文件不能少

void main()
{

     LARGE_INTEGER   litmp;  
     LONGLONG   QPart1,QPart2;  
     double   dfMinus,   dfFreq,   dfTim;  
     QueryPerformanceFrequency(&litmp);                        //获得计数器的时钟频率  
     dfFreq   =   (double)litmp.QuadPart;  
     QueryPerformanceCounter(&litmp);                               //获得初始值
     QPart1   =   litmp.QuadPart;

     QueryPerformanceCounter(&litmp);                        //获得终止值  
     QPart2   =   litmp.QuadPart;
     dfMinus   =   (double)(QPart2-QPart1);
     dfTim   =   dfMinus   /   dfFreq;

     printf( "Time to run this program is %f CPU_Clock\n",dfMinus);
     printf( "Time to run this program is %f seconds\n",dfTim);
}
{% endhighlight %}

这两种方法有时候还会出现负值，可能是使用的时间太长，溢出了。
