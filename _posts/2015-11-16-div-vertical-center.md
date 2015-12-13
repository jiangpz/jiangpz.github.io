---
layout: post
title: div垂直居中
excerpt: "HTML中使用CSS设置div居中显示."
categories: CSS
tags: [CSS, HTML]
date: 2015-11-16 18:08:03 +0800
comments: true
---
---

先是使用的这种方法进行垂直居中：

{% highlight css linenos %}
.vertical-center{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
{% endhighlight %}


但是在IE8中显示时错误的，改用下面的方式进行垂直位置调整了：

{% highlight css linenos %}
.vertical-center{
    margin-left: auto;
    margin-right: auto;
    margin-top: 10%;
}
{% endhighlight %}

可恶的IE.
