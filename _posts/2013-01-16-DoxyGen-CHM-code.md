---
layout: post
title:  "DoxyGen生成的html制作成CHM后目录为乱码的问题"
excerpt: "DoxyGen生成的html制作成CHM后目录为乱码的问题."
date:   2013-01-16 21:30:12 +0800
categories: DoxyGen
tags: [DoxyGen]
comments: true
---
---

我用Dxygen生成的HTML文档，用HTML Help Workshop制作成CHM文件之后，目录居然是乱码的。不知道是什么原因。

Doxyfile里面，所有编码都是设置为GBK的，但是生成的文件居然是UTF-8的格式，也许是因为生成HTMl的相关文件是UTF-8的缘故吧？

不管怎样，总要找到一个解决乱码的方法。其实解决方法很简单：

将 CHM_INDEX_ENCODING 设置为 'GBK' 就可以了.
