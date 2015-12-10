---
layout: post
title: PowerDesigner反向生成ER图
excerpt: "利用powerdesigner反向数据库结构，生成ER图."
categories: PowerDesigner
tags: [PowerDesigner, ER]
date: 2015-07-02 18:00:00 +0800
comments: true
---
---

参考[月下狼~图腾~](http://zhangzhongjie.iteye.com/):《[利用powerdesigner反向数据库结构，生成ER图](http://zhangzhongjie.iteye.com/blog/982539)》

1. 首先新建一个“PhysicalDataModel”类型的文件，然后点击“Database”->"Configure  Connections",弹出窗口“Configure Data Connections”, 并选择"Connection Profiles"如下图所示：  
![1.1](http://ww1.sinaimg.cn/large/4dd787e4gw1etkzgrjjb1j20fa0cjdhb.jpg)  

2. 点击
![2.1](http://ww4.sinaimg.cn/large/4dd787e4gw1etkzgrtn2wj200s00m0mc.jpg)
进行新建一个mysql连接，出现如下窗口：  
![2.2](http://ww3.sinaimg.cn/large/4dd787e4gw1etkzgs6flsj20e40d6dhj.jpg)  

3. 填写连接相关信息，填写完毕后如下图所示：  
![2.3](http://ww2.sinaimg.cn/large/4dd787e4gw1etkzgsm6d3j20e40d676x.jpg)  
（上图相关信息填写需注意：
<1>User name：和Password:为数据库的用户名和密码；
<2>JDBC driver jar files:为你的ojdbc14.jar所在位置，点击后面的图标选择即可。D:\Tools\Oracle\app\Administrator\product\11.2.0\dbhome_1\owb\wf\lib\ojdbc14.jar）

4. 填写完相关信息后点击左下角的“Test Connection... ”进行测试连接是否连接成功。  
![2.4](http://ww2.sinaimg.cn/large/4dd787e4gw1etkzgt6ikaj20b004ogm2.jpg)  
若连接成功，点击“OK”时弹出如下窗口。  
![2.5](http://ww2.sinaimg.cn/large/4dd787e4gw1etkzgtrntpj20hl0g5wi0.jpg)  
若连接不成功，则需要配置ojdbc14.jar的环境变量，过程如下：  
![2.6](http://ww4.sinaimg.cn/large/4dd787e4gw1etkzgw6hxhj20px0huq8t.jpg)  

5. 连接成功后，点击“Database”->"Update Model from  Database(快捷键为：CTRL_R)",弹出窗口“Database Reverse Engineering Options”,如下图所示：  
![5.1](http://ww4.sinaimg.cn/large/4dd787e4gw1etkzgunb8jj20ri0lpn35.jpg)  
完成配置后，弹出如下窗口：  
![5.2](http://ww3.sinaimg.cn/large/4dd787e4gw1etkzgv5imuj20dy0cmad6.jpg)  
选择需要进行反向工程的数据库或数据库中的某些表，然后点击“OK”即可完成数据库的反向工程操作。   （注意：默认是所有数据库全部选中的，所以在进行选择需要进行反向工程的数据库之前，先点击
![5.3](http://ww1.sinaimg.cn/large/4dd787e4gw1etkzgvjw7dj200y00k0ly.jpg)
使得数据库全部未选中。）  
到目前为止，Powerdesigner的反向工程的连接环境全部配置完成，此时只需选中需要进行反向工程的数据库或表，点击“OK”便可导出数据的PhysicalDataModel图。

---
 [@Jpz][writer]
2015 年 07月 02日

[writer]: http://blog.sina.com.cn/u/1305970660
