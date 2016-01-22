---
layout: post
title:  "JavaScript中判断字符串是否以固定字符开始"
excerpt: "JavaScript中判断字符串是否以固定字符开始.可以使用startsWith，但是存在兼容性问题。"
date:   2016-01-22 11:46:21 +0800
categories: JavaScript
tags: [J2EE, JavaScript, IE兼容性]
---

JavaScript中判断字符串是否以固定字符开始.可以使用startsWith，但是存在兼容性问题。

使用ECMAScript 6中的String.prototype.startsWith()方法，其代码如下：

{% highlight js lineos %}
function stringStartsWith (string, prefix) {
    return prefix == '' || string.startsWith(prefix);
}
{% endhighlight %}

但是[并不是所有的浏览器都支持这个方法](http://kangax.github.io/compat-table/es6/#test-String.prototype_methods_String.prototype.startsWith)，尤其是很多国产浏览器都使用的是比较旧的IE内核。

为了兼容IE浏览器，我们使用如下代码：

{% highlight js lineos %}
function stringStartsWith (string, prefix) {
    return string.slice(0, prefix.length) == prefix;
}
{% endhighlight %}

还有许多其他方法，例如

{% highlight js lineos %}
function startsWithCharAt(string, pattern) {
	for (var i = 0, length = pattern.length; i < length; i += 1) {
		if (pattern.charAt(i) !== string.charAt(i)) return false;
	}
	return true;
}
{% endhighlight %}

和

{% highlight js lineos %}
function startsWithArray(string, pattern) {
	for (var i = 0, length = pattern.length; i < length; i += 1) {
		if (pattern[i] !== string[i]) return false;
	}
	return true;
}
{% endhighlight %}

同理，如果要判断字符串是否以指定字符串结尾，可按照如下方法写：

{% highlight js lineos %}
function stringEndsWith (string, suffix) {
    return suffix == '' || string.slice(-suffix.length) == suffix;
}
{% endhighlight %}
