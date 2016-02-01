---
layout: post
title:  "《GPU高性能编程-CUDA实战》中例子头文件使用"
excerpt: "《GPU高性能编程-CUDA实战》中例子头文件使用."
date:   2012-12-20 20:45:12 +0800
categories: CUDA
tags: [CUDA]
---
---

《GPU高性能编程-CUDA实战（CUDA By Example）》中例子中使用的一些头文件是CUDA中和C中本身没有的，需要先下载这本书的源码，可以在：https://developer.nvidia.com/content/cuda-example-introduction-general-purpose-gpu-programming-0 这个网页中下载，点击[Download source code for the book's examples (.zip)](https://developer.nvidia.com/sites/default/files/akamai/cuda/files/cuda_by_example.zip)。
下载后把“cuda_by_example.Zip”中“common文件夹”解压缩到目录：`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v5.0\`下；把“bin文件夹”里的文件glut32.dll和glut64.dll复制到目录：`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v5.0\bin`下；把“lib文件夹”里的文件glut32.lib和glut64.lib复制到目录：`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v5.0\lib\Win32`下。
设置之后就可以像书中例子那样包含头文件了。
