---
layout: post
title:  "Eclipse安装Java反编译插件"
excerpt: "Eclipse中安装Java反编译插件，用于调试与查看源码。"
date:   2016-04-08 17:26:08 +0800
categories: Eclipse
tags: [Eclipse]
---

JD(Java Decompiler)分为JD-GUI、JD-Eclipse、JD-IntelliJ三种运行方式，JD-GUI是以单独的程序的方式运行，JD-Eclipse是以一个Eclipse插件的方式运行，JD-IntelliJ是以一个IntelliJ IDEA插件的方式运行。

JD-GUI在查看和搜索Java源码时很方便，但是在调试程序时，还是需要源码来不能确定每个变量的值。在没有源码时，就需要JD-Eclipse，这个插件可以在debug的过程中显示Java源码，可以设置断点。

#### 下载地址
[jd-eclipse-site-1.0.0-RC2.zip](https://github.com/java-decompiler/jd-eclipse/releases/download/v1.0.0/jd-eclipse-site-1.0.0-RC2.zip)

#### 源码地址
[github.com/java-decompiler/jd-eclipse](https://github.com/java-decompiler/jd-eclipse)

#### 安装过程

1. 下载jd-eclipse-site-1.0.0-RC2.zip
2. 启动Eclipse
3. 点击```Help > Install New Software...```
4. 点击```Add...```添加一个新的仓库
5. 在```Name```中填写"JD-Eclipse Update Site"，点击```Archive...```选择刚刚下载的jar包
6. 勾选"Java Decompiler Eclipse Plug-in"
7. 下一步，下一步，下一步...最后重启Eclipse。
