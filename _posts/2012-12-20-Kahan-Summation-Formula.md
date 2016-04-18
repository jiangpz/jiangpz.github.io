---
layout: post
title:  "Kahan's Summation Formula"
excerpt: "Kahan's Summation Formula."
date:   2012-12-20 15:30:12 +0800
categories: CUDA
tags: [CUDA]
comments: true
---
---


在CUDA的矩阵乘法编程中涉及到了float数组使用到了Kahan's Summation Formula来提高精度：

{% highlight c linenos %}
if(row < n && column < n) {
    float t = 0;
    float y = 0;

    for(i = 0; i < n; i++) {
        float r;
        y -= a[row * lda + i] * b[i * ldb + column];
        r = t - y;
        y = (r - t) + y;
        t = r;
    }
}
{% endhighlight %}

计算结果的误差偏高的原因是，在 CPU 上进行计算时，我们使用 double(即 64 bits 浮点数)来累进计算过程，而在GPU 上则只能用 float(32 bits 浮点数)。在累加大量数字的时候，由于累加结果很快会变大，因此后面的数字很容易被舍去过多的位数。

{% highlight c linenos %}
#include "stdafx.h"
int _tmain(int argc, _TCHAR* argv[])
{
    int i;
    float x=0.001;
    float y;
    float t;
    float sum;
    float eps=0;

    printf("\n理论值：%f\n",x*1000000);

    sum=0;
    for(i=0;i<1000000;i++)
    {
        sum+=x;
    }
    printf("\n累加值：%f\n",sum);

    sum=0;
    for(i=0;i<1000000;i++)
    {
        y=x-eps;
        t=sum+y;
        eps=(t-sum)-y;
        sum=t;
    }
    printf("\nKahan累加值：%f\n",sum);

    getchar();
    return 0;
}
{% endhighlight %}

保持精度的小trick：Kahan求和
由于最近用GPU编程，涉及到了float数组，就不得不涉及精度问题。对于双精度如C中double以及Fortran中real(kind = 8)，一般运算的精度足以保持，但是单精度数组，在大量操作后极易出现“大数吃小数”等不稳定现象。在不能使用更高精度数组的前提下，可以用一个小技巧来保持精度：Kahan求和。

1 见下面一段Fortran代码：

{% highlight c fortran %}
program main
implicit none
    integer, parameter:: N = 1000000
    integer i
    real(kind = 4), parameter:: ELEMENT = 0.001
    real(kind = 4) s, eps, y, t

    write (*, "('Theoretical value: ', F10.5)") N*ELEMENT

    s = 0.0
    do i = 1, N
        s = s+ELEMENT
    enddo
    write (*, "('Naive method value: ', F10.5)") s

   s = 0.0
    eps = 0.0
    do i = 1, N
        y = ELEMENT-eps
        t = s+y
        eps = (t-s)-y
        s = t
    enddo
    write (*, "('Kahan method value: ',F10.5)") s

stop
end
{% endhighlight %}

运行结果为：

{% highlight text %}
Theoretical value: 1000.00006
Naive method value:  991.14154
Kahan method value: 1000.00006
{% endhighlight %}

对于N个0.001，普通方法累加到991左右就已经丢失精度了。可以看到用“Kahan method”能够得到近乎于理论的精度数值。分析一下他的原理。我们发现，如果没有精度损失，eps永远为0，y就是ELEMENT=0.001。一旦在 i 到了某个数值出现了大数吃小数 的情形时，不妨激进的设小数部分全部被截断，则如s = 991.0000时，由于eps之前为0，则y=0.0010.之后t=s+y，得到的就是“吃掉”的结果，如991.0000，绝对误差达0.001.此时：eps=(t-s)-y=(991.0000-991.0000)-0.0010=-0.001，可见eps起了保存“损失位”的作用。此时s=t=991.0000.下个循环：y = 0.001--0.001=0.002，t = s+y=991.0000，eps=-0.002，如此反复，这样足够多循环后，eps足可以复现大的校正值，从而保证结果的高精度。当eps足够大时候，(t-s)-y=0,从而使eps重新为0，继续起保存损失的作用。
例如，在GPU计算大型矩阵或向量时，如果涉及到reduction操作，可以在加和中使用这种技巧。当然GPU计算能力在2.x是可以有双精度运算，但是要比单精度慢20倍左右，一般不经常使用。
