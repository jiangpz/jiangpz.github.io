---
layout: post
title:  "无法定位程序输入点_glutCreateWindowWithExit于动态链接库glut32.dll"
excerpt: "在使用《GPU高性能编程-CUDA实战》中例子在运行时会遇到“无法定位程序输入点_glutCreateWindowWithExit于动态链接库glut32.dll”的报错."
date:   2013-03-13 15:53:46 +0800
categories: CUDA
tags: [CUDA]
comments: true
---
---

在使用《GPU高性能编程-CUDA实战》中例子在运行时会遇到“无法定位程序输入点_glutCreateWindowWithExit于动态链接库glut32.dll”的报错，网友说是glut.dll文件太老了，解决方法如下：

0. 在OpenGl官网上下载了[glut3.7](http://www.opengl.org/resources/libraries/glut/glutdlls37beta.zip)。

1. 将原来在C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA下增加的文件夹common下的gl文件夹下的glut.h删除，把下载的glut3.7的glut.h加到这个文件夹下；

2. 把C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v5.0\bin下的glut32.dll和glut64.dll删除，把glut3.7的glut32.dll和glut.dll加到这个文件夹下；

3. 把C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v5.0\lib\Win32下的glut32.lib和glut64.lib删除，把glut3.7的glut32.lib 和glut.lib 加到这个文件夹下。

4. 然后重新生成解决方案就可以了。
