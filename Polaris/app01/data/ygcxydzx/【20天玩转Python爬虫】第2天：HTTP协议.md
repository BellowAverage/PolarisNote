
--- 
title:  【20天玩转Python爬虫】第2天：HTTP协议 
tags: []
categories: [] 

---
我们学习知识就像盖房子一样，没有良好的地基，房子经不起风吹雨打。而如果房子的地基搭建的足够牢固，即使台风来了都是高高的耸立在那里。

我们没有上来就讲爬虫怎么用，而是讲了一些基础的内容，这些内容大家都掌握了，后面我们学习实操爬虫就会很顺利，很清晰了。

## HTTP协议

提到爬虫我们不得不提起HTTP协议，那什么是HTTP协议呢？HTTP协议(超文本传输协议HyperText Transfer Protocol)，它是基于TCP协议的应用层传输协议，简单来说就是客户端和服务端进行数据传输的一种规则。

 - 超文本：是指超过文本，不仅限于文本；还包括图片、音频、视频等文件
 - 传输协议：是指使用共用约定的固定格式来传递转换成字符串的超文本内容
 - 默认端口号：80

并且HTTP是一种无状态(stateless) 协议，HTTP协议本身不会对发送过的请求和相应的通信状态进行持久化处理。这样做的目的是为了保持HTTP协议的简单性，从而能够快速处理大量的事务，提高效率。有时我们还会使用到https协议，其实他是HTTP + SSL(安全套接字层)，即带有安全套接字层的超本文传输协，默认端口号：443

 - SSL对传输的内容（超文本，也就是请求体或响应体）进行加密

## 请求

HTTP协议中每次请求都会携带下方的内容，比如有请求的方法、请求的路径、协议的版本等我们称作**请求行**

还有符合字段名：值的这个方式的，我们称作请求头。

最后一部分是请求体。

<img alt="" height="233" src="https://img-blog.csdnimg.cn/20210618100213879.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lnY3h5ZHp4,size_16,color_FFFFFF,t_70" width="646">

大家来看一下，浏览器的开发者工具Network中的请求情况：
