---
layout: post
title: 工作环境安装与配置说明
excerpt: "本文档对三部的开发环境的系统安装、软件安装与配置进行说明."
categories: Work
tags: [Work]
date: 2015-06-02 18:00:00 +0800
comments: true
---
---

本文档对三部的开发环境的系统安装、软件安装与配置进行说明。

##### 一、系统版本
Windows 7 旗舰版 Service Pack 1 64 位操作系统

##### 二、系统安装
原计划直接Ghost一个镜像，里面有系统、驱动、软件，但是由于开发使用的硬件不同，就没有再详细做这件事情，现在有一个可以直接就开始开发的Ghost，配合公司的旧电脑。好吧，我承认，用安装程序直接安装挺迅速的，所以我放弃Ghost，写了这篇软件安装手册。系统安装不再详述，基本技能。
在公司系统需要配置IP地址，
这时候还有个关于科学上网的问题，[Google全球缓存IP—中国红客联盟](http://g.ihonker.org/)好久没更新了，还是去[老D博客](http://laod.cn/hosts/2015-google-hosts.html)看看吧，或者掏些小钱用[HelloDNS](http://www.hellodns.org/),至于其他工具就不用了，我们只是为了用谷歌。

##### 三、软件安装列表
1. Cmd Markdown

一个Markdown编辑器，本文也是使用此编辑器编辑的。Markdown的语法简洁明了、学习容易，而且功能比纯文本更强，因此有很多人用它写博客。用于编写说明文档，并且以“README.MD”(注意这个扩展名噢，你一定会再遇到，因为有缘[^footnote1])的文件名保存在软件的目录下面。由于Markdown具有一系列衍生版本，用于扩展Markdown的功能，其语法兼容性较差，所以使用统一编辑器查看方便些，这是一款在线的编辑器，所以不怕丢失，易于分享[^footnote2]，缺点就是如果分享了任何人都能看到。

2. 360安全卫士

大家都知道360是个流氓，但是，自从见识过百度之后，才知道什么是真流氓，好了，我们把360请回来，用软件管家安装软件，优化开机速度，当然，360也是不开机启动的(可怜的办公笔记本内存)。

3. IE 10 浏览器

使用IE进行系统开发，要求所开发的系统支持IE8+，将系统自动的IE9升级为IE10即可，也可以下载安装包安装。[Firefox](http://www.firefox.com.cn/)在debug时使用[Firefox 开发工具](https://developer.mozilla.org/zh-CN/docs/Tools)比较方便，Chrome调整页面方便，我用的遨游最大的好处是云同步和页面另存为图片。

安装位置：默认位置

4. Foxmail

用于接收邮件，如果你喜欢Outlook，也可以的，请根据自身情况选择，如果是公司破旧的笔记本，就选择Foxmail吧。安装完成后记得配置账号。我得找乔帮主要一份通讯录！

5. iSee图片专家

用于查看和编辑图片。你有其他喜欢的图片查看和编辑工具也可以的，自由选择。

文件关联：所有格式

6. Beyond Compare 3

强悍的文件与文件夹对比工具。

破解：见BCompare-zh-3.3.5.15075.txt

7. Microsoft Office

Office系列软件。需要安装Excel、PowerPoint、Word、Visio，OutLook、Onenote等可根据需要选装。

版本：2013

破解：HEU_KMS_Activator_v7.8.8.exe

8. Notepad++

优秀的文本查看工具，写jsp也很适用，其实我更推荐[Sublime Text 2](http://www.sublimetext.com/2)，[Sublime Text 3](http://www.sublimetext.com/3)还是测试版。多位置编辑太好用了，Sublime Text 2是收费软件，但可以无限期试用。和Sublime很像而且免费的是Atom，速度慢些，可以试试他的Active Power Mode插件，很酷。[HBuilder](http://dcloud.io/)也是很好的编辑工具，语法提示完善，顺便可以学学[Emmet](http://www.iteye.com/news/27580)。

9. Java Development Kit（JDK）

  [java开发环境](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)。

  版本：1.6.0_37（32位）

  位置：C:\Program Files\Java\jdk1.6.0_37(路径中最好不要有空格)

  配置环境变量：[见“配置JAVA的环境变量_百度经验.pdf”](http://jingyan.baidu.com/article/f96699bb8b38e0894e3c1bef.html)

    现在有个问题，新版本java不配置环境变量，java -version和java命令可用，javac不可用没搞清楚

10.  Eclipse

    [Eclipse.org](http://download.eclipse.org/)。Eclipse与JDK应该都为32位或64位。

  版本：Eclipse IDE for Java EE Developers 32位

  位置：


	10.Orcal数据库
		开发适用的数据库。
		版本：11g
		位置：
		安装方法：

	11.PLSQL Developer
		PL/SQL Developer面向于Oracle数据库的存储单元开发，其主要侧重于代码的品质及易用性，可以充分发挥出Oracle程序的开发优势。
		版本：10
		破解：相关注册码.txt

	12.PowerDesigner
		反向生成ER图。
		版本：15
		破解：Readme.txt
		使用方法：

	13.TongLINKQ 与 TongLINKQ WebManager
		TongLINKQ为数据交换中间件。TongLINKQ WebManager为TLQ的Web管理工具，需要在IE8模式下进行操作。
		版本：8.1.1.5(8.1.2.8)
		安装方法与破解：

	14.TortoiseSVN
		SVN版本管理工具。项目中版本管理使用Git类工具，项目的相关资料文档使用SVN管理。
		使用方法：

	15.7-Zip
		解压缩工具。

	16.福昕阅读器
		pdf阅读器，可根据自己喜欢选择。

	17.QQ
		请加群：实施三部 310390974、水利事业部（DHCC） 171662509。

	18.AxureRPProPortable
		网站原型设计工具。
		版本：6.5 绿色版
		位置：C:\Program Files\AxureRPProPortable

	19.SecureCRSecureFXPortable
		远程连接Linux。

	20.Maven
		版本：3.1.1
		配置：



	22.Tomcat
		版本：6.0.35
		位置：

	23.搜狗输入法
		总得有个输入法吧。

	1.VMware
		虚拟机。安装XP系统用于测试IE8的兼容性，CentOS用于部署服务和在Linux环境下进行测试。
		版本：10.0.0 build-1295980

	2.Chrome 浏览器 （ 选装 ）
		安装Chrome浏览器，用于程序开发Debug和多浏览器支持。
		版本：
		位置：

	3.FireFox 浏览器 （ 选装 ）
		安装FireFox浏览器，用于程序开发Debug和多浏览器支持。
		版本：
		位置：

	4.EverNote （ 选装 ）
		便签，可在不同系统上同步。

	5.HP LoadRunner
		测试工具。

	6.MySQL数据库
		系统未来要支持MySQL数据库。

	7.Weblogic
		用于发布服务。

	8.TongWeb5.0
		TongWeb是一个符合J2EE规范的应用服务器产品，相当于Weblogic。

	9.Convert Oracle to Mysql
		将Orcal数据库中数据导入到Mysql中。
		版本：
		位置：
		文件关联：

	10.字体
		MONACO.TTF

	11. RealVNC
		远程控制和远程监控软件。

##### 五、有用的网站
	1.科学上网IP：http://googless.sinaapp.com/
	2.公司SVN的Web地址：https://10.10.116.188:8443/svn/
	3.开源中国Git：http://git.oschina.net/
	4.jQuery API：http://api.jquery.com/
	          中文文档：http://www.css88.com/jqapi-1.9/
	5.常用在线工具：http://tool.oschina.net/
	6.ACE，项目中使用的框架 ：http://static.weixiaodeyu.com/html5/admin-template/ace/
	7.RGB颜色查询对照表：http://www.114la.com/other/rgb.htm
	8.EGit用户手册（英文版）：http://wiki.eclipse.org/EGit/User_Guide

##### 六、公司服务器
	1.公司打印机IP： 10.10.181.250
	                  型号：惠普HP LaserJet 5200LX
	                  驱动：upd-pcl6-x64-5.9.0.18326.exe

  2.公司协同：http://xt.dhcc.com.cn/

  3.公司邮箱：http://mail.dhcc.com.cn

  4.公司wifi：名称： slszy 密码：63207254szy

  5.公司服务器：10.10.116.243  
	           用户名：root   
             密码：slszyadmin123  
        tongWeb：http://10.10.116.243:9060/twns/login.jsf  
          用户名：twns  
            密码：twns  
            位置：/opt/app/app_wars  

    6.SVN客户端更新地址：https://10.10.116.188:8443/svn/WSD_SVN/，用户名密码是姓名全拼

【关于软件版本号】
我们的格式为： Vx.x.x(yymmdd)。其中x可以任意位数数字。
每次升级，如果是修改功能或者改bug，最后一位+1 。如果加减功能第2位+1 ,大的逻辑和架构变化（ui变化，合同二期等），第1位+1.
后面括号里面6位是时间 yymmdd，每次升级编译的时候改成编译时的时间！


一定要改，要不我们的点太多，升级太频繁，最后版本不一致带来的问题扯皮的事情就太多了。

---
 [@Jpz][writer]
2015 年 06月 02日

[writer]: http://blog.sina.com.cn/u/1305970660

[^footnote1]: 在许多Git项目中，会建立一个README.MD的文档对项目进行说明，这个文档一般是使用Markdown语法编写的，包括本文档。

[^footnote2]: 本文在线地址https://www.zybuluo.com/Jpz/note/108401
