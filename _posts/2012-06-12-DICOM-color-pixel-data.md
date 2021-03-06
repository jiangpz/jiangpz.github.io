---
layout: post
title:  "判断DICOM图像类型获取像素数据与DICOM格式介绍"
excerpt: "判断DICOM图像是单色的还是彩色的与如何获取DICOM图像的像素数据，介绍DICOM文件头与数据集合."
date:   2012-06-12 21:30:12 +0800
categories: DICOM
tags: [DICOM]
comments: true
---
---

### 判断图像是单色的还是彩色的
根据0028,0004（Photometric   Interpretation）决定，如果是MONOCHROME1或MONOCHROME2就是灰度的，如果是RGB则是RGB，还有其他可能。
还应该参考

{% highlight text %}
 0028,0100   BitsAllocated  
 0028,0002   SamplePerPixel
{% endhighlight %}

等决定位数。

### 如何获取图像的像素数据
从7FE0,0010(Pixel Data)得到像素数据就可以了。

### DICOM文件头

DICOM文件头(DICOM File Meta Information)包含了标识数据集合的相关信息。每个DICOM文件都必须包括该文件头。文件头的最开始是文件前言，它由128个00H字节组成，接下来是DICOM前缀，它是一个长度为4字节的字符串“DICM”，可以根据该值来判断一个文件是不是DICOM文件。文件头中还包括其它一些非常有用的信息，如文件的传输格式、生成该文件的应用程序等等，关于文件头详细的说明请参阅DICOM标准PS 3.10的13~14页表7.1-1。

说明:

1.  除了128字节的文件前言和4字节的DICOM前缀外，所有其它的文件头元素都必须采用上面介绍的显示格式编码，各个数据元素排列的顺序按照标签数值从小到大的传输格式(Little Endian)编码。

2. 每个文件头元素的长度必须为偶数，否则应该按照规定补充一个字节。

3. 所有(0002，****)类的标签都为DICOM所保留。为了兼容后续版本，如果发现文件中有目前尚未规定的(0002，****)类标签，则应该忽略它。

### DICOM数据集合

DICOM文件主要组成部分就是数据集合。这不仅包括医学图像，还包括许多和医学图像有关的信息，如病人姓名、图像大小等。

DICOM数据集合是由DICOM数据元素按照指定的顺序依次排列组成的。对于DICOM文件，一般采用显式传输，数据元素按标签从小到大顺序排列，即DICOM PS 3.5规定的Explicit VR Little En-dian Transfer Syntax。

在DIOCM标准的PS 3.3部分(Information Object Defini-tions)中，定义了各种类型的图像文件必须包括和可选的DICOM数据元素，在制定自己的DICOM文件结构时，必须严格遵照该部分规定。例如，制定核磁共振医学图像的DICOM文件，可以查阅DICOM标准PS 3.3中的A.4节。其中定义了如下的核磁共振医学图像信息实体(Information Entity，IE)的内容(表4)。

表中“使用”列为“M”时表示该模块必须存在，“U”表示可选，“C”表示在特定的情况下必须存在。

要构造信息实体，按照表中指定的模块参考相应的DICOM标准章节即可。例如，在制定Patient模块时，查阅DICOM标准PS 3.3部分的C.7.1.1小节，可以查到如表5所示的病人模块属性表。

这样按照表5中所列出的元素，选出自己需要的元素(表中类型为1和2的元素是必须包括的，3可选)即可。按照表4中指出的所有模块，查阅DICOM标准中相应的章节，选出合适的DICOM元素，这样DICOM文件的格式就确定下来了。
