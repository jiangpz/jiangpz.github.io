---
layout: post
title:  "关于CUDA中cutil的一些问题"
excerpt: "由于Cuda 5.0不支持cutil.h，需要用helper_cuda.h等文件代替cutil.h."
date:   2013-01-09 19:00:42 +0800
categories: CUDA
tags: [CUDA]
comments: true
---
---

在编译其他人的CUDA程序中经常遇到一些与cutil相关的文件不能找到的问题，像cutil.h、cutil_inline.h、cutil_gl_inline.h、cutil_gl_error.h、cutil_match.h等文件，这是因为5.0版本的Cuda不支持cutil.h 文件了。

> Prior to CUDA 5.0, CUDA Sample projects referenced a utility lib rary with header and source files called cuti l. This has been removed with the CUDA Samples in CUDA 5.0, and re placed with header files found in CUDA Samples \ v5.0 \ common \ inc helper_cuda.h, helper_cuda_ gl.h, helper_cuda_drvapi.h, helper_functions.h, helper_image.h, helper_math.h, help er_string.h, and helper_timer.h .These files provide utility functions f or CUDA device initialization, CUDA error checking, string parsing, imag e file loading and saving, and timing functions. The CUDA Samples proj ects no longer have references and dependencies to cutil, and will now use these helper functions going forward.

helper_cuda.h等文件可以在下面的[网站查看](http://mlso.hao.ucar.edu/hao/acos/sw/cuda-sdk/CUDALibraries/common/inc/)。

至于找不到GL/glew.h，要包含C:\ProgramData\NVIDIA Corporation\CUDA Samples\v5.0\common\inc\GL 这个文件夹。
