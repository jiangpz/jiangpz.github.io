---
layout: post
title: GitHub Flavored Markdown
excerpt: "对Standard Markdown和GitHub Flavored Markdown进行介绍，来自官方文档."
categories: Linux
tags: [terminal, Linux]
date: 2015-08-02 18:00:00 +0800
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

```
# The largest heading (an <h1> tag)
## The second largest heading (an <h2> tag)
…
###### The 6th largest heading (an <h6> tag)
```

的效果如下：

# The largest heading
## The second largest heading
…
###### The 6th largest heading

###### 引用

使用`<`来引用。例如：

```
In the words of Abraham Lincoln:

> Pardon my french
```

效果如下

In the words of Abraham Lincoln:

> Pardon my french

###### 字体样式

可以使字体变为*粗体*或者**斜体**。例如

```
*This text will be italic*

**This text will be bold**
```

效果如下：

*This text will be italic*

**This text will be bold**

可以使用`*`或者`_`来使用*粗体*或者**斜体**，这样就可以将粗体和斜体结合使用。例如：

```
**Everyone _must_ attend the meeting at 5 o'clock today.**
```

效果如下：

**Everyone _must_ attend the meeting at 5 o'clock today.**

###### 无序列表

可以使用`*`或者`_`来创建无序列表。如下：

```
* Item
* Item
* Item

- Item
- Item
- Item
```

效果如下：
* Item
* Item
* Item

- Item
- Item
- Item

###### 有序列表

可以通过在列表条目前增加`数字+.`来创建一个有序列表，如下：

```
1. Item 1
2. Item 2
3. Item 3
```

效果如下

1. Item 1
2. Item 2
3. Item 3

###### 嵌套列表

通过列表项缩进两个空格，可以创建嵌套列表，如下

```
1. Item 1
  1. A corollary to the above item.
  2. Yet another point to consider.
2. Item 2
  * A corollary that does not need to be ordered.
    * This is indented four spaces, because it's two spaces further than the item above.
    * You might want to consider making a new list.
3. Item 3
```

效果如下：

1. Item 1
  1. A corollary to the above item.
  2. Yet another point to consider.
2. Item 2
  * A corollary that does not need to be ordered.
    * This is indented four spaces, because it's two spaces further than the item above.
    * You might want to consider making a new list.
3. Item 3

###### 代码样式

内联代码

使用反引号`` ` ``包裹代码，这些代码中不会再显示其他特殊样式,例如：

```
Here's an idea: why don't we take `SuperiorProject` and turn it into `**Reasonable**Project`.
```

效果如下：

Here's an idea: why don't we take `SuperiorProject` and turn it into `**Reasonable**Project`.

多行代码

如果插入多行代码，使用三个反引号```` ``` ````，例如：

````
Check out this neat program I wrote:

```
x = 0
x = 2 + 2
what is x
```
````

效果如下：

Check out this neat program I wrote:

```
x = 0
x = 2 + 2
what is x
```

其实在在插入代码时，只要用N个反引号包裹就可以，开始和结束反引号个数相同，要超过代码中间如果包含的连续反引号个数就可以了。

在Github上，可以使用语法高亮，例如：

````
```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```
````

效果如下：

```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

也可以直接在代码前增加四个空格来实现插入代码：

```
    function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }
```

效果如下：

    function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }    

在写github pages时，在jekyll中使用pygments来实现代码高亮，如下：

```
{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}
```

效果如下：

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

其中`linenos`是用来显示行号，`ruby`用来指定语言类型，具体可以参照[pygments官网说明](http://pygments.org/docs/lexers/)

###### 链接

如果创建链接，链接文字用` [ ] `包裹，后面紧跟用` ( ) `包裹的链接地址，例如：

```
[Visit GitHub!](https://www.github.com)
```

效果如下：

[Visit GitHub!](https://www.github.com)


###### 图片

插入图片和插入链接相识，需要在前面增加一个`!`，例如：

```
If you want to embed images, this is how you do it:

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)
```

效果如下：

If you want to embed images, this is how you do it:

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)




###### 链接

###### 链接

###### 链接

###### 链接

###### 链接

###### 链接

###### 链接




- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> are supported
- [x] list syntax is required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item

---
 [@Jpz][writer]
2015 年 08月 02日

[writer]: http://blog.sina.com.cn/u/1305970660

[Markdown_Basics]: http://blog.sina.com.cn/u/1305970660
