
--- 
title:  Nmap使用详解_nmap使用教程 
tags: []
categories: [] 

---
##### 一、Nmap介绍

<img src="https://img-blog.csdnimg.cn/20210225160534331.png" alt="">Nmap(Network Mapper，网络映射器)是一款开放源代码的网络探测和安全审核工具。它被设计用来快速扫描大型网络，包括主机探测与发现、开放的端口情况、操作系统与应用服务指纹识别、WAF识别及常见安全漏洞。它的图形化界面是Zenmap，分布式框架为DNmap。

###### 1、Nmap的特点如下：
-  主机探测：探测网络上的主机，如列出响应TCP和ICMP请求、ICMP请求、开放特别端口的主机。 -  端口扫描：探测目标主机所开放的端口。 -  版本检测：探测目标主机的网络服务，判断其服务名称及版本号。 -  系统检测:探测目标主机的操作系统及网络设备的硬件特性。 -  支持探测脚本的编写:使用Nmap的脚本引擎(NSE)和Lua编程语言。 
##### 二、安装Nmap

Windows中Nmap下载地址：<img src="https://img-blog.csdnimg.cn/20210225162039690.png" alt=""> 在安装的过程中按照提示一步步进行即可 <img src="https://img-blog.csdnimg.cn/20210225162723148.png" alt=""> 安装完成后可以直接通过命令行使用 <img src="https://img-blog.csdnimg.cn/20210225164014744.png" alt="">

##### 三、Nmap常用方法

Nmap的参数较多，但是通常用不了那么多，以下是在渗透测试过程中比较常见的命令。

###### 1、扫描单个目标地址：

在Nmap后面直接添加目标地址即可扫描，如下所示：

```
nmap 192.168.0.100


```

<img src="https://img-blog.csdnimg.cn/2021022821521149.png" alt="在这里插入图片描述">

###### 2、扫描多个目标地址：

如果目标地址不在同一网段，或在同一网段但不连续且数量不多，可以使用该方法进行扫描，如下所示：

```
nmap 192.168.0.1 192.168.0.6


```

<img src="https://img-blog.csdnimg.cn/2021022822003825.png" alt="在这里插入图片描述">

###### 3、扫描一个范围内的目标地址：

可以指定扫描一个连续的网段，中间使用“-”连接，例如，下列命令表示扫描范围为192.168.0.1~192.168.0.6，如下所示：

```
nmap 192.168.0.1-6


```

<img src="https://img-blog.csdnimg.cn/20210228220838312.png" alt="在这里插入图片描述">

###### 4、扫描目标地址所在的某个网段：

以C段为例，如果目标是一个网段，则可以通过添加子网掩码的方式扫描，下列命令表示扫描范围为192.168.0.1～192.168.0.255，如下所示：

```
nmap 192.168.0.1/24


```

<img src="https://img-blog.csdnimg.cn/20210228221059968.png" alt="在这里插入图片描述">

###### 5、扫描主机列表targets.txt中的所有目标地址：

扫描 targets.txt 中的地址或者网段，此处导入的是绝对路径，如果 targets.txt 文件与 nmap.exe 在同一个目录下，则直接引用文件名即可，如下所示：

```
nmap -iL C:\Users\smk\Desktop\targets.txt


```

<img src="https://img-blog.csdnimg.cn/20210228222647502.png" alt="在这里插入图片描述">

###### 6、扫描除某一个目标地址之外的所有目标地址：

下列命令表示扫描除192.168.0.105之外的其他192.168.0.x地址，从扫描结果来看确实没有对192.168.0.105进行扫描，如下所示：

```
nmap 192.168.0.100/24 -exclude 192.168.0.1


```

<img src="https://img-blog.csdnimg.cn/20210228223048405.png" alt="在这里插入图片描述">

###### 7、扫描除某一文件中的目标地址之外的目标地址：

下列命令表示扫描除了target.txt文件夹中涉及的地址或网段之外的目标地址。还是以扫描192.168.0.x网段为例，在targets.txt中添加192.168.0.100和192.168.0.105，从扫描结果来看已经证实该方法有效可用，如下所示：

```
nmap 192.168.0.100/24 -excludefile C:\Users\smk\Desktop\targets.txt


```

<img src="https://img-blog.csdnimg.cn/20210228223717135.png" alt="在这里插入图片描述">

###### 8、-p 扫描某一目标地址的21、22、23、80端口：

如果不需要对目标主机进行全端口扫描，只想探测它是否开放了某一端口，那么使用-p参数指定端口号，将大大提升扫描速度，如下所示：

```
nmap 192.168.0.6 -p 135,443,445


```

>  
 -p : 只扫描指定的端口，-p-代表全端口扫描 


<img src="https://img-blog.csdnimg.cn/20210228231610466.png" alt="在这里插入图片描述">

###### 9、–traceroute 路由跟踪：

下列命令表示对目标地址进行路由跟踪，如下所示：

```
nmap --traceroute 192.168.0.6


```

###### 10、-sP 所在C段的在线状况：

下列命令表示扫描目标地址所在C段的在线状况，如下所示：

```
nmap -sP 192.168.0.100/24


```

<img src="https://img-blog.csdnimg.cn/20210301001240550.png" alt="在这里插入图片描述">

###### 11、-O 操作系统识别：

下列命令表示通过指纹识别技术识别目标地址的操作系统的版本，如下所示：

```
nmap -O 192.168.0.6


```

<img src="https://img-blog.csdnimg.cn/20210301001440818.png" alt="在这里插入图片描述">

###### 12、-Pn 跳过Ping扫描（无ping扫描）：

```
nmap -Pn 192.168.1.1


```

###### 13、-sV 版本探测：

```
nmap -sV 192.168.1.1


```

<img src="https://img-blog.csdnimg.cn/c5abcc6718da40208d45bf4d7589af72.png" alt="在这里插入图片描述">

###### 14、-sn 只单独进行主机发现过程

###### 15、扫描目标所开放的全部端口（半开式）

nmap -sS -p 端口号(多个用逗号隔开) ip

-sS：半开扫描，很少有系统能把它记入系统日志。不过，需要Root权限。

```
nmap -sS -p 1-65535 192.168.0.101


```

## 学习资料分享

当然，**只给予计划不给予学习资料的行为无异于耍流氓**，### 如果你对网络安全入门感兴趣，那么你点击这里**👉**

**如果你对网络安全感兴趣，学习资源免费分享，保证100%免费！！！（嘿客入门教程）**

**👉网安（嘿客）全套学习视频👈**

我们在看视频学习的时候，不能光动眼动脑不动手，比较科学的学习方法是在理解之后运用它们，这时候练手项目就很适合了。

#### 

#### <img src="https://img-blog.csdnimg.cn/img_convert/d1c617b78ee48eda7601e5b803e69276.png" alt="img">

#### **👉网安（嘿客红蓝对抗）所有方向的学习路线****👈**

对于从来没有接触过网络安全的同学，我们帮你准备了详细的学习成长路线图。可以说是最科学最系统的学习路线，大家跟着这个大的方向学习准没问题。

#### <img src="https://img-blog.csdnimg.cn/img_convert/de55dfd737dae0cf88e416d0454b17a8.png" alt="img">

#### 学习资料工具包

压箱底的好资料，全面地介绍网络安全的基础理论，包括逆向、八层网络防御、汇编语言、白帽子web安全、密码学、网络安全协议等，将基础理论和主流工具的应用实践紧密结合，有利于读者理解各种主流工具背后的实现机制。

<img src="https://img-blog.csdnimg.cn/9609a53465cf4253b492a5185896fa71.png" alt="在这里插入图片描述">

**面试题资料**

独家渠道收集京东、360、天融信等公司测试题！进大厂指日可待！ <img src="https://img-blog.csdnimg.cn/f5f267c281c543fb9cc9af53b9003a37.png" alt="在这里插入图片描述">

#### **👉<strong><strong>嘿客必备开发工具**</strong>👈</strong>

工欲善其事必先利其器。学习**嘿**客常用的开发软件都在这里了，给大家节省了很多时间。

#### 这份完整版的网络安全（**嘿**客）全套学习资料已经上传至CSDN官方，朋友们如果需要点击下方链接**也可扫描下方微信二v码获取网络工程师全套资料**【保证100%免费】

#### <img src="https://img-blog.csdnimg.cn/img_convert/16c400294b6fda8f01400f24f1f12b0c.png" alt="在这里插入图片描述">

#### 如果你对网络安全入门感兴趣，那么你点击这里**👉**
