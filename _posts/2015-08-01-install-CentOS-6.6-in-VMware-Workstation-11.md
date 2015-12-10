---
layout: post
title: VMware Workstation 11中CentOS 6.6安装
excerpt: "安装完CentOS 6.6系统之后，我们需要设置终端的快捷键."
categories: Linux
tags: [CentOS, Linux, VMware]
date: 2015-08-01 18:00:00 +0800
comments: true
---
---

> 如果人生的途程上没有障碍，人还有什么可做的呢。  ——俾斯麦

最近计划把开发环境从windows上迁移到Linux上，希望在平时做开发的时候也能够熟悉linux环境，这个过程将会遇到很多问题，包括Linux发行版选择与安装、开发环境配置和windows常用工具的代替等等，这些问题都必须得到解决并记下来。

#####Linux发行版选择

Linux发行版数量很多，可以在[distrowatch.com](http://distrowatch.com/)上看到他们的排名，Debian、Ubuntu、Fedora、CentOS是我安装过的Linux的发行版，点击量第一的Mint我没有使用过，据说使用起来很方便，和XP很像，适用于家庭用户和企业办公。
想在这么多版本中选择一个是很难的，光是看介绍就要花费很长时间，也不会有人去一一尝试，只需要根据自己的需要，选择一个合适的就行。
我选择CentOS的原因如下：

1. 《鸟哥的Linux私房菜基础学习篇》的作者，大名鼎鼎的[鸟哥](http://vbird.dic.ksu.edu.tw/)使用的CentOS，所以不用再发愁学习Linux的资料了，而且也不用再买书了，去[鸟哥的Linux私房菜简体首页](http://vbird.dic.ksu.edu.tw/)，啥都有。CentOS使用的人比较多，遇到问题可以在网上很快寻找到解决方法。  

2. 我们更多是为了学习Linux服务器，现在国内服务器中红帽的使用量是很大的，而CentOs来自于Red Hat Enterprise Linux，依照其开放源代码规定释出的源代码所编译而成。由于出自同样的源代码，因此有些要求高度稳定性的服务器以CentOS替代商业版的Red Hat Enterprise Linux使用。去看看[GNU/Linux Distribution Timeline](http://futurist.se/gldt/wp-content/uploads/12.10/gldt1210.png)就知道他们有多近。

3. 熟练掌握了一个发行版，再去学习另外一个，将会是很简单的事情，因为原理相同，总是纠结版本不如先拿一个试试手。


#####CentOS安装
由于从Windows转到CentOS，中间需要很长的尝试时间，因此先使用虚拟机安装CentOS，我使用的是VMware Workstation 11，要安装的CentOS版本是6.6，因为CentOS 6和现在服务器上的系统很接近。CentOS 7中的变化还是挺大的，但是还没开始广泛使用，暂且不用。
在此安装过程中我们不使用简易安装。下载地址是[http://wiki.centos.org/Download](http://wiki.centos.org/Download)。

1. 安装VMware Workstation 11。网上很多[教程](http://www.jb51.net/softjc/255389.html)，也很简单。

2. 启动Mware Workstation 11，点击“创建新的虚拟机”。  
![](http://ww3.sinaimg.cn/large/4dd787e4jw1euok2zgat8j210a0l2q7a.jpg)

3. 在弹出对话框中选择“自定义”，然后点击“下一步”。  
![](http://ww4.sinaimg.cn/large/4dd787e4jw1euok302ayyj20iz0hwdi3.jpg)

4. 选择硬件兼容性，使用默认即可，点击“下一步”  
![](http://ww4.sinaimg.cn/large/4dd787e4jw1euok30bjzaj20iz0hwq4l.jpg)

5. 选择“稍后安装操作系统”，点击“下一步”。如果现在“选择安装程序光盘映像文件”，就会使用简易安装。  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok30o4pmj20iz0hwdhq.jpg)

6. 客户机操作系统选择“Linux”，版本选择“CentOS 64 位”，大家可根据自己要安装的系统，自行选择。点击“下一步”。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok3168p6j20iz0hwwg8.jpg)

7. 给虚拟机命名并选择安装位置。  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok31dss4j20iz0hw75p.jpg)

8. 选择处理器配置。当然是处理器的总核数越多，运行的越快，在保证主机运行良好的前提下，核数越多，虚拟机性能越高。但是如果“处理器数量”与“每个处理器的核心数量”的乘积超过主机的线程数，例如我的电脑是2核4线程，那么这个乘积就不能超过4。可以去计算机管理中看看处理器的个数，不超过这个个数就可以。  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok31ohglj20iz0hw0tw.jpg)

9. 设置内存大小，根据主机可用内存进行设置。点击右侧的数字，例如“2 GB”，就可以设置为2GB。点击“下一步”。  
![](http://ww2.sinaimg.cn/mw690/4dd787e4jw1euok321ai2j20iz0hw0v0.jpg)

10. 选择[网络类型](http://blog.sina.com.cn/s/blog_4dd787e40101e49u.html)。桥接：基于链路层协议将两个通信网络互连，说通俗点就是把同一网段中的设备用交换机互联。在vmware workstation中虚拟网卡VMnet0的默认属性为桥接
NAT：网络地址转换(NAT,Network Address Translation)的简称，通常用于Internet接入。在vmware workstation中虚拟网卡VMnet8的默认属性为NAT，并且默认启用了dhcp，通常用于虚拟机上ingernet的一种方式。
Host-only：这种技术提供了主机和虚拟机、虚拟机和虚拟机之前的网络通信，而不是虚拟机访问Internet，在这种模式下相当于使虚拟机和主机、虚拟机和虚拟机处在一个和外网隔离的网络中。在vmware workstation中虚拟网卡VMnet1的默认属性为Host-only。在家里用的无线路由器，就使用桥接网络了。点击“下一步”。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok32btugj20iz0hw0uu.jpg)

11. I/O控制器使用默认类型，点击“下一步”。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok32ne7aj20iz0hwgn1.jpg)

12. 磁盘类型使用默认值，点击“下一步”。  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok3323ouj20iz0hwwgx.jpg)

13. 选择“创建新虚拟硬盘”，点击“下一步”。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok339tztj20iz0hwmz5.jpg)

14. 我们制定硬盘大小为“40GB”，其实本身CentOS并不需要这么大空间，这是为安装软件预留的，同时，我们还不希望现在就开始学习磁盘扩充。为了提高性能，我们选择“立即分配所有磁盘空间”和“将虚拟磁盘存储为单个文件”，点击“下一步”。  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok3323ouj20iz0hwwgx.jpg)

15. 使用默认值，点击“下一步”。  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok33kvpdj20iz0hwdh4.jpg)

16. 这时虚拟机配置基本完成，点击自定义硬件：  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok33tizpj20iz0hwtb4.jpg)
将安装盘放到虚拟光驱中，选择“新 CD/DVD”，选择“使用ISO映像文件”，如果下载了两个DVD，放进去DVD1就可以。
点击“关闭”。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok347tnaj20sk0p0777.jpg)

17. 点击“完成”。这时会创建磁盘，需要等待一些时间。创建好后如下图所示。  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok34nusxj210a0l2q8x.jpg)

18. 点击“开启此虚拟机”。如果弹出：  
![](http://ww2.sinaimg.cn/mw690/4dd787e4jw1euok34z0hij20cy09ewfo.jpg)
点击确定就行

19. 选择第一个“Install or upgrade an existing system”，不要选择第二个，因为选择第二个，那么安装时就看不到下方的“下一步”和上一步。当鼠标点击虚拟机界面后，鼠标就默认在虚拟机界面里移动，想将鼠标从虚拟机中释放出来，需要同时按下“Ctrl”和“Alt”。我们选中第一项后回车。  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok35ddn5j20hu0dctb0.jpg)

20. 等待出现如下界面：  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok35my6yj20k20b475g.jpg)
用方向键选择“Skip”

21. 之后出现如下界面，点击“next”。  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok35z7ffj20m60gft9r.jpg)

22. 选择语言，我们就用英语吧。点击“next”。  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok36cbjmj20m70gqwg3.jpg)

23. 选择键盘，选择“U.S.English”。点击“next”  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok36l0j6j20m80gcq45.jpg)

24. 选择“Basic Storage Devices”。点击“next”  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok36x553j20mb0gumyb.jpg)

25. 选择“Yes， discard any data”。  
![](http://ww2.sinaimg.cn/mw690/4dd787e4jw1euok37hp90j20md0hw76q.jpg)

26. 主机名使用默认值，点击“next”  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok37rknhj20m60gpwf6.jpg)

27. 选择时区，我们选择上海，点击“next”  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok38373yj20m90grmzk.jpg)

28. Root密码，上下两个输入框各输入一次，只是六位，写好了要记住。点击“next”
![]()
如果密码是弱密码，会提示是否继续使用密码，选择“Use Anyway”。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok38nho7j20m90gqdgz.jpg)

29. 分区，选择“Use All Apace”，点击“next”。如果像鸟哥那样进行复杂的自定义分区，请选择“Use Custom Layout”，具体的参考[鸟哥的教程吧](http://vbird.dic.ksu.edu.tw/linux_basic/0157installcentos5_2.php)。  
![](http://ww2.sinaimg.cn/mw690/4dd787e4jw1euok38ywmhj20m80gpaca.jpg)

30. 选择“Write changes to disk”  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok39a4ttj20m50ghwfc.jpg)

31. 在这里选择要安装的软件，先选择“Desktop”，然后选择“Customize now”，点击“next”  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok3aadzgj20mb0gmmz3.jpg)

32. 选择要安装的软件，在“Languages”中选择“Chines Support”和“English Support”，“Applicants”里可以多选择几个，其他的按默认就行，所需软件在实际使用的时候，需要安装再安装，现在安装的版本可能与以后使用的版本不同。点击“next”  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok3amz5jj20m40gmgns.jpg)

33. 然后是漫长的等待。   ![](http://ww2.sinaimg.cn/mw690/4dd787e4jw1euok3ayo4ej20ma0gn75m.jpg)  
设置一下电脑的电源选项，不要休眠了。安装完成后点击Reboot。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok3bf6uoj20m90gmq3z.jpg)

34. 进入欢迎界面，点击“Forward”  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok3brwm9j20zf0l640i.jpg)

35. License选Yes，点击“Forward”  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok3c53xmj20zi0lc0us.jpg)

36. 填写用户名密码，此用户不是root用户，没有超级管理员权限。点击“Forward”  
![](http://ww1.sinaimg.cn/mw690/4dd787e4jw1euok3chp9yj20zm0l9mzo.jpg)

37. 设置时间。点击“Forward”  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok3cwxd4j20zd0l9jtu.jpg)

38. kdump是在系统崩溃、死锁或者死机的时候用来转储内存运行参数的一个工具和服务，打个比方，如果系统一旦崩溃那么正常的内核就没有办法工作了，在这个时候将由kdump产生一个用于capture当前运行信息的内核，该内核会将此时的内存中的所有运行状态和数据信息收集到一个dump core文件中以便于Red Hat工程师分析崩溃原因，一旦内存信息收集完成，系统将自动重启。这和以前的diskdump，netdump是同样道理。只不过kdump是RHEL5特有的。使用默认值，点击“Finish”，弹出框中点“Yes”，再弹出框中再点“Yes”，然后重启。  
![](http://ww4.sinaimg.cn/mw690/4dd787e4jw1euok3d9nx2j20zg0l542o.jpg)

39. 选择用户，填写密码，然后“Log In”。在这个界面下方是可以选择语言的。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok3dm3vtj20zb0l876k.jpg)

40. 可以使用了。  
![](http://ww2.sinaimg.cn/mw690/4dd787e4jw1euok3e641pj20zm0lf0ww.jpg)

#####Vmware Tools安装
VMware Tools是VMware虚拟机中自带的一种增强工具，相当于VirtualBox中的增强功能（Sun VirtualBox Guest Additions），是VMware提供的增强虚拟显卡和硬盘性能、以及同步虚拟机与主机时钟的驱动程序。
只有在VMware虚拟机中安装好了VMware Tools，才能实现主机与虚拟机之间的文件共享，同时可支持自由拖拽的功能，鼠标也可在虚拟机与主机之前自由移动（不用再按ctrl+alt），且虚拟机屏幕也可实现全屏化。
1. 单击“虚拟机”菜单下的“安装VMware-Tools”。  
![]()  

2. 选择“Applications”→“System Tools”→“Terminal”，  
![](http://ww2.sinaimg.cn/mw690/4dd787e4jw1euok3e641pj20zm0lf0ww.jpg)输入`su`，回车，再输入密码，密码为上面步骤28中的密码。  
![](http://ww3.sinaimg.cn/mw690/4dd787e4jw1euok3ehg5ij20ii0d1wf3.jpg)

3. 输入`ls /media/VMware\ Tools/`,回车，会看到有Vmwaretools的.rpm和.tar.gz的包

4. 输入`cp /media/VMware\ Tools/VMwareTools*.tar.gz /tmp/`,回车，将VMware Tools拷贝到tmp文件夹下

5. 输入`cd /tmp/`，回车，切换到tmp目录

6. 输入`tar -zxvf Vmware*.tar.gz`,回车，解压文件

7. 输入`cd vmware-tools-distrib`，回车，切换到VMware Tools目录

8. 输入`./vmware-install.pl`,回车

9. 一直按回车,当你看到终端出现“Searching for GCC…”那一句命令后，不再按回车了，输入“no”，接下来它又会出现一句，其中有一句“would you like to change it?”，也输入“no”,其实一直按回车也没问题的

10. 一直按“回车”

11. 当终端出现“Enjoy， –the VMware team”就表示VMware tools安装好了。在终端输入“exit”关闭终端窗口

12. 输入`reboot`重启，现在已经可以随意地在虚拟机和电脑之间拖放文件了

#####结束语
现在CentOS安装完成了，下一步需要配置一下输入法、Terminal的快捷键、开发环境等等。

---
 [@Jpz][writer]
2015 年 08月 01日

[writer]: http://blog.sina.com.cn/u/1305970660
