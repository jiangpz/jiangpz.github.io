---
layout: post
title: "Customizing Your Blog"
excerpt: "关于博客头信息的说明."
categories: MAC
tags: [terminal, iTerm2, OS X]
date: 2015-04-29 21:32:27 +0800
comments: true
---
对头信息进行说明：

layout: 如果设置的话，会指定使用该模板文件。指定模板文件时候不需要扩展名。模板文件需要放在`_layouts`目录下。一般博客中设置为`post`。    
title: 文章标题，用双引号包裹。例如`"Customizing Your iTerm2"`。  
excerpt: 文章摘要，一般用一小段话对文章内容进行描述，如果有`excerpt`，那么在主要的文章列表中，文章标题下会显示这段描述，否则会显示整篇文章，建议进行设置，例如`"Just about everything you'll need to customize your iTerm2 or the default Mac OS X Terminal."`。  
categories: 文章分类，一般只写一个分类，不用双引号包裹，例如`MAC`。Jekyll官方文档上说可以用空格分隔多个分类。  
tags: 文章标签，一个文章可以有多个便签，便于查找，用中括号包裹，用逗号分隔，例如`[terminal, iTerm2, OS X]`。
date: 文章发表时间，文章列表将按照发表时候排序，格式如下`2015-11-26 16:46:21 +0800`。  
comments: 为评论的插件，还未启用，与disqus-shortname有关，等以后再加上去。现在设置为`true`。  
