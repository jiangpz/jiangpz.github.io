---
layout: post
title:  "在Linux中TongWeb乱码与重启TongWeb:ps、kill"
excerpt: "修改TongWeb默认编码与TongWeb重启方法."
date:   2015-12-29 15:46:21 +0800
categories: Linux
tags: [Linux, TongWeb]
---

在使用TongWeb中经常会出现乱码，我们的项目默认使用UTF-8编码，而TongWeb默认使用的编码是GBK。修改完编码后TongWeb是需要重启的，可是TongWeb可不是个省心的中间件。

#### 修改TongWeb编码

修改TongWeb编码需要修改tongweb的配置文件TongWeb6.0/conf/tongweb.xml，修改对应端口（如果端口是8080，就修改端口号为8080的）的http-listener的uri-encoding，如果是GBK现在改成UTF-8。

使用vi打开配置文件：

{% highlight sh %}
vi /home/TongWeb6.0/conf/tongweb.xml
{% endhighlight %}

打开后找到这http-listener，将其中的uri-encoding改为UTF-8，如下：

{% highlight xml %}
<http-listener name="tong-http-listener" port="8080" uri-encoding="UTF-8" parse-body-methods="POST,DELETE,PUT" default-virtual-host="server" create-time="2015-12-24 15:18:50">
    <ssl/>
    <protocol/>
    <http-options/>
    <advance/>
</http-listener>
{% endhighlight %}

修改之后保存退出。

#### 停止TongWeb

停止TongWeb时一般先运行stopserver.sh：

{% highlight sh %}
[root@weblogic01 ~]# /home/TongWeb6.0/bin/stopserver.sh
[2015-12-29 11:19:12] [WARNING] [System.out] [log4j:WARN No appenders could be found for logger (com.tongweb.commons.modeler.BaseModelMBean).]
[2015-12-29 11:19:12] [WARNING] [System.out] [log4j:WARN Please initialize the log4j system properly.]
{% endhighlight %}

但是这样是不能够彻底停止TongWeb的进程的。所以在运行stopserver.sh之后，我们查看现在系统进程中是否还有TongWeb，使用`ps aux | grep tong`(ps这个命令在下面详述):

{% highlight sh %}
[root@weblogic01 ~]# ps aux | grep tong
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root      50465  0.0  0.0 103256   852 pts/0    S+   11:19   0:00 grep tong
root      71983  0.4  3.8 10811676 2552512 ?    Sl   Dec25  27:10 /home/jdk1.6.0_45/bin/java -classpath /home/jdk1.6.0_45/lib/tools.jar:/home/TongWeb6.0/lib/launcher.jar -Xms5120m -Xmx5120m -XX:MaxPermSize=1024m -XX:+UnlockDiagnosticVMOptions -XX:+LogVMOutput -Djava.security.auth.login.config=/home/TongWeb6.0/conf/security/login.config -Djava.util.logging.manager=com.tongweb.log.TongwebLogManager -Djava.endorsed.dirs=/home/TongWeb6.0/lib/endorsed -Dtongweb.jndi.lookup.relaxVersion=false -Djava.security.egd=file:/dev/./urandom -Djava.rmi.server.RMIClassLoaderSpi=com.tongweb.server.TongWebRMIClassLoader -javaagent:/home/TongWeb6.0/lib/tongejb-javaagent.jar -Djava.awt.headless=true -Dibm.stream.nio=true -Djava.net.preferIPv4Stack=true -XX:LogFile=/home/TongWeb6.0/logs/jvm.log -Dcom.tongweb.commons.logging.Log=com.tongweb.commons.logging.impl.Jdk14Logger -Dtongweb.java=/home/jdk1.6.0_45 -Dtongweb.upload=/home/TongWeb6.0/temp/upload -Dtongweb.app=/home/TongWeb6.0/deployment -Dtongweb.sysapp=/home/TongWeb6.0/applications -Dtongweb.home=/home/TongWeb6.0 -Djava.io.tmpdir=/home/TongWeb6.0/temp -Dtongweb.snapshotinhour=5 com.tongweb.web.thor.startup.ThorBootstrap start
{% endhighlight %}

其中第二列为PID，可以看到PID为71983的与TongWeb相关的进程并没有停止。使用`kill`结束这个进程(kill这个命令在下面详述):

{% highlight sh %}
[root@weblogic01 ~]# kill -9 71983
[root@weblogic01 ~]# ps aux | grep tong
root      50489  0.0  0.0 103256   848 pts/0    S+   11:19   0:00 grep tong
{% endhighlight %}

#### 启动TongWeb

启动TongWeb比较简单，使用nohup(nohup的使用方法详见[Linux命令：nohup、df、du与/dev/null](http://jiangpz.github.io/articles/2015-11/Linux-nohup-df-du-dev-null)),需要注意“&”的位置，不要少空格，在运行成功后敲一个回车再退出终端:

{% highlight sh %}
[root@weblogic01 ~]# nohup /home/TongWeb6.0/bin/startserver.sh & > /dev/null
[1] 50753
[root@weblogic01 ~]# nohup: 蹇界暐杈撳叆骞舵妸杈撳嚭杩藉姞鍒nohup.out"

[root@weblogic01 ~]#
{% endhighlight %}

#### ps

##### ps命令参数
 - ps a    显示现行终端机下的所有程序，包括其他用户的程序。
 - ps -A   显示所有程序。
 - ps c    列出程序时，显示每个程序真正的指令名称，而不包含路径，参数或常驻服务的标示。
 - ps -e   此参数的效果和指定"A"参数相同。
 - ps e    列出程序时，显示每个程序所使用的环境变量。
 - ps f    用ASCII字符显示树状结构，表达程序间的相互关系。
 - ps -H    显示树状结构，表示程序间的相互关系。
 - ps -N   显示所有的程序，除了执行ps指令终端机下的程序之外。
 - ps s     采用程序信号的格式显示程序状况。
 - ps S     列出程序时，包括已中断的子程序资料。
 - ps -t <终端机编号> 　指定终端机编号，并列出属于该终端机的程序的状况。
 - ps u 　 以用户为主的格式来显示程序状况。
 - ps x 　 显示所有程序，不以终端机来区分。
 - ps -l   较长,较详细的显示该PID的信息

##### ps aux相关信息的意义

 - USER：该进程属于那个使用者账号的？
 - PID ：该进程的进程ID号。
 - %CPU：该进程使用掉的 CPU 资源百分比；
 - %MEM：该进程所占用的物理内存百分比；
 - VSZ ：该进程使用掉的虚拟内存量 (Kbytes)
 - RSS ：该进程占用的固定的内存量 (Kbytes)
 - TTY ：该进程是在那个终端机上面运作，若与终端机无关，则显示 ?，另外， tty1-tty6 是本机上面的登入者程序，若为 pts/0 等等的，则表示为由网络连接进主机的程序。
 - STAT：该程序目前的状态，主要的状态有：
     - R ：该程序目前正在运作，或者是可被运作；
     - S ：该程序目前正在睡眠当中 (可说是 idle 状态啦！)，但可被某些讯号(signal) 唤醒。
     - T ：该程序目前正在侦测或者是停止了；
     - Z ：该程序应该已经终止，但是其父程序却无法正常的终止他，造成 zombie (疆尸) 程序的状态
 - START：该进程被触发启动的时间；
 - TIME ：该进程实际使用 CPU 运作的时间。
 - COMMAND：该程序的实际指令为什么？

#### kill

Linux中的kill命令用来终止指定的进程（terminate a process）的运行，是Linux下进程管理的常用命令。通常，终止一个前台进程可以使用Ctrl+C键，但是，对于一个后台进程就须用kill命令来终止，我们就需要先使用ps/pidof/pstree/top等工具获取进程PID，然后使用kill命令来杀掉该进程。kill命令是通过向进程发送指定的信号来结束相应进程的。在默认情况下，采用编号为15的TERM信号。TERM信号将终止所有不能捕获该信号的进程。对于那些可以捕获该信号的进程就要用编号为9的kill信号，强行“杀掉”该进程。

##### 命令格式

kill [-s 信号编码|-p] [--] pid...
kill -l [信号编码]

##### 命令功能

发送指定的信号到相应进程。不指定型号将发送SIGTERM（15）终止指定进程。如果任无法终止该程序可用“-KILL” 参数，其发送的信号为SIGKILL(9) ，将强制结束进程，使用ps命令或者jobs 命令可以查看进程号。root用户将影响用户的进程，非root用户只能影响自己的进程。

##### 命令参数

 - kill -l  信号，若果不加信号的编号参数，则使用“-l”参数会列出全部的信号名称
 - kill -a  当处理当前进程时，不限制命令名和进程号的对应关系
 - kill -p  指定kill 命令只打印相关进程的进程号，而不发送任何信号
 - kill -s  指定发送信号
 - kill -u  指定用户

##### 使用举例

 - 列出所有信号名称：kill -l
 - 彻底杀死pid为123456的进程：kill –9 123456
 - 杀死指定用户peidalinux所有进程：kill -9 $(ps -ef | grep peidalinux)或者kill -u peidalinux
