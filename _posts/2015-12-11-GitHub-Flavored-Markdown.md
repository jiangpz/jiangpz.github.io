---
layout: post
title: GitHub Flavored Markdown
excerpt: "对Standard Markdown(SM)和GitHub Flavored Markdown(GFM)进行介绍，来自官方文档."
categories: Markdown
tags: [Markdown, Jekyll]
date: 2015-12-11 18:00:00 +0800
comments: true
---
---

##### 参考文献

- [Markdown Basics-https://help.github.com/articles/markdown-basics/](https://help.github.com/articles/markdown-basics/)
- [Mastering Markdown-https://guides.github.com/features/mastering-markdown/](https://guides.github.com/features/mastering-markdown/)

##### Markdown基础

###### 段落

在Markdown中段落是一行或者多行字符后有一个或者多个空行。也就是说每个段落中用一个或者多个空行分隔。

###### 标题

通过再在标题文字前增加一个个或者多个`#`来形成标题。`#`的数量决定了标题的大小，例如：

{% highlight text %}
# The largest heading (an <h1> tag)
## The second largest heading (an <h2> tag)
…
###### The 6th largest heading (an <h6> tag)
{% endhighlight %}

的效果如下：

# The largest heading

## The second largest heading

…

###### The 6th largest heading


###### 引用

使用`<`来引用。例如：

{% highlight text %}
In the words of Abraham Lincoln:
> Pardon my french
{% endhighlight %}

效果如下

In the words of Abraham Lincoln:

> Pardon my french

###### 字体样式

可以使字体变为*粗体*或者**斜体**。例如

{% highlight text %}
*This text will be italic*

**This text will be bold**
{% endhighlight %}

效果如下：

*This text will be italic*

**This text will be bold**

可以使用`*`或者`_`来使用*粗体*或者**斜体**，这样就可以将粗体和斜体结合使用。例如：

{% highlight text %}
**Everyone _must_ attend the meeting at 5 o'clock today.**
{% endhighlight %}

效果如下：

**Everyone _must_ attend the meeting at 5 o'clock today.**

###### 无序列表

可以使用`*`或者`_`来创建无序列表。如下：

{% highlight text %}
* Item
* Item
* Item

- Item
- Item
- Item
{% endhighlight %}

效果如下：

* Item
* Item
* Item



- Item
- Item
- Item

###### 有序列表

可以通过在列表条目前增加`数字+.`来创建一个有序列表，如下：

{% highlight text %}
1. Item 1
2. Item 2
3. Item 3
{% endhighlight %}

效果如下

1. Item 1
2. Item 2
3. Item 3

###### 嵌套列表

通过列表项缩进两个空格，可以创建嵌套列表，如下

{% highlight text %}
1. Item 1
    1. A corollary to the above item.
    2. Yet another point to consider.
2. Item 2
    * A corollary that does not need to be ordered.
        * This is indented four spaces, because it's two spaces further than the item above.
        * You might want to consider making a new list.
3. Item 3
{% endhighlight %}

效果如下：

1. Item 1
    1. A corollary to the above item.
    2. Yet another point to consider.
2. Item 2
    * A corollary that does not need to be ordered.
        * This is indented four spaces, because it's two spaces further than the item above.
        * You might want to consider making a new list.
3. Item 3

在使用Atom进行编辑时，发现需要空四个空格，应该是Atom做了一些转换，使用四个空格保险些吧。

###### 代码样式

内联代码

使用反引号`` ` ``包裹代码，这些代码中不会再显示其他特殊样式,例如：

{% highlight text %}
Here's an idea: why don't we take `SuperiorProject` and turn it into `**Reasonable**Project`.
{% endhighlight %}

效果如下：

Here's an idea: why don't we take `SuperiorProject` and turn it into `**Reasonable**Project`.

多行代码

如果插入多行代码，使用三个反引号```` ``` ````，例如：

{% highlight text %}
Check out this neat program I wrote:

```
x = 0
x = 2 + 2
what is x
```
{% endhighlight %}

效果如下：

Check out this neat program I wrote:

{% highlight text %}
x = 0
x = 2 + 2
what is x
{% endhighlight %}

其实在在插入代码时，只要用N个反引号包裹就可以，开始和结束反引号个数相同，要超过代码中间如果包含的连续反引号个数就可以了。

在Github上，可以使用语法高亮，例如：

{% highlight text %}
```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```
{% endhighlight %}

效果如下：

{% highlight js %}
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
{% endhighlight %}

也可以直接在代码前增加四个空格来实现插入代码：

{% highlight text %}
    function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }
{% endhighlight %}

效果如下：

{% highlight text %}
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}    
{% endhighlight %}

在写github pages时，在jekyll中使用pygments来实现代码高亮，如下(百分号前的斜杠是转义字符，粘贴时实际应该去掉)：

{% highlight text %}
{\% highlight ruby linenos \%}
def foo
  puts 'foo'
end
{\% endhighlight \%}
{% endhighlight %}

效果如下：

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

其中`linenos`是用来显示行号，`ruby`用来指定语言类型，具体可以参照[pygments官网说明](http://pygments.org/docs/lexers/)。
需要注意的是，在写github pages需要用pygments来实现代码块增加，不能使用:

{% highlight text %}
```
XXXXXX
```
{% endhighlight %}

###### 链接

如果创建链接，链接文字用` [ ] `包裹，后面紧跟用` ( ) `包裹的链接地址，例如：

{% highlight text %}
[Visit GitHub!](https://www.github.com)
{% endhighlight %}

效果如下：

[Visit GitHub!](https://www.github.com)


###### 图片

插入图片和插入链接相识，需要在前面增加一个`!`，例如：

{% highlight text %}
If you want to embed images, this is how you do it:

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)
{% endhighlight %}

效果如下：

If you want to embed images, this is how you do it:

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)

###### 表格

可通过如下方式增加表格：列名用`|`分隔，第二行使用破折号`-`填充，例如：

{% highlight text %}
First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell
{% endhighlight %}

为了审美的要求，可以在前后加上冗余的`|`:

{% highlight text %}
| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |
{% endhighlight %}

破折号`-`的长度不需要和表头相同:

{% highlight text %}
| Name | Description          |
| ------------- | ----------- |
| Help      | Display the help window.|
| Close     | Closes a window     |
{% endhighlight %}

可以在表格中使用其他Markdown语法，例如链接、粗体、斜体、删除线:

{% highlight text %}
| Name | Description          |
| ------------- | ----------- |
| Help      | ~~Display the~~ help window.|
| Close     | _Closes_ a window     |
{% endhighlight %}

效果如下：

| Name | Description          |
| ------------- | ----------- |
| Help      | ~~Display the~~ help window.|
| Close     | _Closes_ a window     |

最后，可以通过冒号`:`设置左对齐、右对齐或者中心对齐：

{% highlight text %}
| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |
{% endhighlight %}

效果如下：

| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |

如果冒号在最左为左对齐，如果冒号在最右为右对齐，如果冒号在两端为中心对齐.


###### 任务列表

GFM中还支持任务列表，Github Pages中不能使用：

{% highlight text %}
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
  - [x] list syntax required (any unordered or ordered list supported)
  - [x] this is a complete item
- [x] this is a complete item
- [ ] this is an incomplete item
{% endhighlight %}

效果如下：

- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
  - [x] list syntax required (any unordered or ordered list supported)
  - [x] this is a complete item
- [x] this is a complete item
- [ ] this is an incomplete item

###### 链接转换

GFM中会将任何URL(例如http://www.github.com/)自动转换成一个可以点击的链接。在Github Pages不会做这个转换。

###### 删除线

GFM中可以增加删除线(例如`~~this~~`)。在Github Pages不会做这个转换。

---
 [@Jpz][writer]
2015 年 12月 11日

[writer]: http://blog.sina.com.cn/u/1305970660
