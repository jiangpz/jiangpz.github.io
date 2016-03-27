---
layout: post
title:  "在CentOS上升级Ruby"
excerpt: "CentOS上使用yum安装的Ruby的版本较低，在用Jekyll写博客时需要升级Ruby。"
date:   2016-03-11 12:44:25 +0800
categories: Linux
tags: [Linux, Ruby]
---

在CentOS中安装Jekyll时，报如下错误

{% highlight sh %}
[root@localhost rubygems-2.6.1]# gem install jekyll
Building native extensions.  This could take a while...
ERROR:  Error installing jekyll:
	ERROR: Failed to build gem native extension.

	    current directory: /usr/lib/ruby/gems/1.8/gems/ffi-1.9.10/ext/ffi_c
		/usr/bin/ruby -r ./siteconf20160311-29821-oqnlp6-0.rb extconf.rb
		mkmf.rb can't find header files for ruby at /usr/lib/ruby/ruby.h

		extconf failed, exit code 1

		Gem files will remain installed in /usr/lib/ruby/gems/1.8/gems/ffi-1.9.10 for inspection.
		Results logged to /usr/lib/ruby/gems/1.8/extensions/x86-linux/1.8/ffi-1.9.10/gem_make.out
{% endhighlight %}

这是由于CentOS中使用YUM安装到Ruby版本太低到原因，CentOS中默认到Ruby版本为1.8.7：

{% highlight sh %}
[root@localhost rubygems-2.6.1]# ruby -v
ruby 1.8.7 (2013-06-27 patchlevel 374) [i386-linux]
{% endhighlight %}

一些Ruby应用需要Ruby 1.9。这时候需要升级Ruby。

如果已经使用yum安装了ruby和ruby-devel，那么在升级之前需要卸载旧版本：

{% highlight sh %}
sudo yum remove ruby ruby-devel
{% endhighlight %}

按照如下到方式编译安装Ruby：

{% highlight sh %}
$ sudo yum groupinstall "Development Tools"
$ sudo yum install openssl-devel
$ wget http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz
$ tar xvfvz ruby-2.1.2.tar.gz
$ cd ruby-2.1.2
$ ./configure
$ make
$ sudo make install
{% endhighlight %}

如果启动Jekyll时报如下错误：

{% highlight sh %}
Yikes! It looks like you don't have pygments or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem.
{% endhighlight %}

则需要安装pygmenys：

{% highlight sh %}
gem install pygments.rb
{% endhighlight %}
