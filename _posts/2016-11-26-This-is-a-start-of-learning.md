---
layout: post
title: 这是一个学习的开始
excerpt: "测试一下Jekyll的代码样式."
date:   2015-11-25 16:46:21 +0800
categories: jekyll update
---

这是一个学习的开始

1. 哈哈
2. 呵呵
3. 嘿嘿
4. 嘻嘻

layout: 如果设置的话，会指定使用该模板文件。指定模板文件时候不需要扩展名。模板文件需要放在`_layouts`目录下。一般博客中设置为`post`。    
title: 文章标题，用双引号包裹。例如`"Customizing Your iTerm2"`。  
excerpt: 文章摘要，一般用一小段话对文章内容进行描述，如果有`excerpt`，那么在主要的文章列表中，文章标题下会显示这段描述，否则会显示整篇文章，建议进行设置，例如`"Just about everything you'll need to customize your iTerm2 or the default Mac OS X Terminal."`。  
categories: 文章分类，一般只写一个分类，不用双引号包裹，例如`MAC`。Jekyll官方文档上说可以用空格分隔多个分类。  
tags: 文章标签，一个文章可以有多个便签，便于查找，用中括号包裹，用逗号分隔，例如`[terminal, iTerm2, OS X]`。
date: 文章发表时间，文章列表将按照发表时候排序，格式如下`2015-11-26 16:46:21 +0800`。  
comments: 为评论的插件，还未启用，与disqus-shortname有关，等以后再加上去。现在设置为`true`。

##我要试试图片

###下面是以前的图片
1. 首先新建一个“PhysicalDataModel”类型的文件，然后点击“Database”->"Configure  Connections",弹出窗口“Configure Data Connections”, 并选择"Connection Profiles"如下图所示：
![1.1](http://ww1.sinaimg.cn/large/4dd787e4gw1etkzgrjjb1j20fa0cjdhb.jpg)
2. 点击![2.1](http://ww4.sinaimg.cn/large/4dd787e4gw1etkzgrtn2wj200s00m0mc.jpg)进行新建一个mysql连接，出现如下窗口：
![2.2](http://ww3.sinaimg.cn/large/4dd787e4gw1etkzgs6flsj20e40d6dhj.jpg)
3. 填写连接相关信息，填写完毕后如下图所示：
![2.3](http://ww2.sinaimg.cn/large/4dd787e4gw1etkzgsm6d3j20e40d676x.jpg)
（上图相关信息填写需注意：
<1>User name：和Password:为数据库的用户名和密码；
<2>JDBC driver jar files:为你的ojdbc14.jar所在位置，点击后面的图标选择即可。D:\Tools\Oracle\app\Administrator\product\11.2.0\dbhome_1\owb\wf\lib\ojdbc14.jar）

###下面是assets下的图片
![有帮助的截图]({{ site.url }}/assets/screenshot.jpg)

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}
  test  
{% highlight ruby linenos %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

  test  
  
{% highlight sql linenos %}

select t10.主小区,
       t10.临小区,
       t10.临小区pn,
       t11.中间临小区 主小区与再临小区的中间小区,
       t10.再临小区,
       t10.再临小区PN
  from (select t9.主小区, t9.临小区, 临小区pn, t8.再临小区, t8.再临小区PN
          from --找到每个小区的再临小区与再临小区PN
               (select t3.主小区, t3.再临小区, t4.pn 再临小区PN
                  from (select t1.主小区, t1.临小区, t2.临小区 再临小区
                          from 小区相邻关系表 t1
                          left join 小区相邻关系表 t2
                            on t1.临小区 = t2.主小区) t3
                  left join 小区与PN对应关系表 t4
                    on t4.小区标志 = t3.再临小区
                 where t3.主小区 != t3.再临小区) t8
          left join
        --找到每个小区的临小区与临小区PN
         (select t6.主小区, t6.临小区, t7.pn 临小区pn
           from 小区相邻关系表 t6
           left join 小区与PN对应关系表 t7
             on t7.小区标志 = t6.临小区) t9
            on t9.主小区 = t8.主小区

         where t9.临小区 != t8.再临小区
           and t9.临小区pn = t8.再临小区PN) t10
  left join (select distinct t3.主小区,
                             t3.中间临小区,
                             t3.再临小区,
                             t4.pn 再临小区PN
               from (select t1.主小区,
                            t1.临小区 中间临小区,
                            t2.临小区 再临小区
                       from 小区相邻关系表 t1
                       left join 小区相邻关系表 t2
                         on t1.临小区 = t2.主小区) t3
               left join 小区与PN对应关系表 t4
                 on t4.小区标志 = t3.再临小区
              where t3.主小区 != t3.再临小区) t11

    on t10.主小区 = t11.主小区
   and t10.再临小区 = t11.再临小区

--xiaoq
{% endhighlight %}
