
--- 
title:  RabbitMQ真实生产故障问题还原与分析 
tags: []
categories: [] 

---
**1、    ****问题引发**

　　由某个服务BI-collector-xx队列出现阻塞，影响很整个rabbitMQ集群服务不可用，多个应用MQ生产者服务出现假死状态，系统影响面较广，业务影响很大。当时为了应急处理，恢复系统可用，运维相对粗暴的把一堆阻塞队列信息清空，然后重启整个集群。RabbitMQ真实生产故障问题还原与分析

在复盘整个故障过程中，我心中有不少疑惑，至少存在以下几个问题点：

 1. 为什么出现队列阻塞？
 1. 某个队列出现阻塞为什么会影响到其他队列的运行（即多队列间相互影响）？
 1. 某个应用MQ队列出现问题，为什么会导致应用不可用呢？



**2、    ****试验队列阻塞**

某天周末在家里，找个测试环境，安装rabbitmq尝试重现这过程，并做模拟测试。

写两个测试应用Demo（假设是两个项目应用）分别有生产者和消费者，并分别使用队列testA和testB。

为了尽可能还原生产的情况，一开始测试使用了同一个vhost，后面分别设置不同vhost。



生产者A，示例代码如下

 

<img alt="" src="https://img-blog.csdnimg.cn/img_convert/774c52564d98c339ff2e3d52647ba225.png">

消费者A

 


