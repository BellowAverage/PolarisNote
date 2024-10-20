
--- 
title:  C语言开发基于RT-Thread家庭安全环境检测系统源码，RTT设计大赛 
tags: []
categories: [] 

---
## 基于RT-Thread家庭安全环境检测

### 简介

基于RT-Thread和中蓝讯科的AB32VG1开发板实现的家庭安全检测功能，主要包含如下功能： 1、基于RT-Thread操作系统的按键组件，音频播放组件等； 2、基于AB32VG1开发板的语音播放功能； 3、基于Node-Red的串口功能与AB32VG1通讯； 4、连接腾讯云的Explorer平台； 5、腾讯连连公众号接收云平报警信息； 6、门窗检测开关。

### 注意事项

芯片有部分不开源的代码是以静态库提供的，静态库在软件包中，默认已勾选，直接运行 `pkgs --update` 即可

波特率默认为 1.5M，需要使用  下载 `.dcf` 到芯片，需要编译后自动下载，需要在 `Downloader` 中的下载的下拉窗中选择 `自动`；目前暂时屏蔽 uart1 打印

使用 `romfs` 时，需要自己生成 `romfs.c` 进行替换，操作参考

编译报错的时候，如果出现重复定义的报错，可能需要在 `cconfig.h` 中手动添加以下配置

```
#define HAVE_SIGEVENT 1
#define HAVE_SIGINFO 1
#define HAVE_SIGVAL 1

```

所有在中断中使用的函数或数据需要放在 RAM 中，否则会导致系统运行报错。具体做法可以参考下面

```
RT_SECTION(".irq.example.str")
static const char example_info[] = "example 0x%x";

RT_SECTION(".irq.example")
void example_isr(void)
{<!-- -->
    rt_kprintf(example_info, 11);
    ...
}

```

### 开发板介绍

ab32vg1-prougen 是 中科蓝讯(Bluetrum) 推出的一款基于 RISC-V 内核的开发板，最高主频为 120Mhz，该开发板芯片为 AB32VG1。

开发板外观如下图所示：

<img src="https://img-blog.csdnimg.cn/f5c1757099b3456ebd8cea6418679e67.png" alt="在这里插入图片描述">

该开发板常用 **板载资源** 如下：
- MCU：AB32VG1，主频 120MHz，可超频至 192MHz，8Mbit FLASH ，192KB RAM。<li>常用外设 
  <ul>- LED: RGB灯- 按键: 3 个, USER(s2,s3) and RESET(s1)
### 外设支持

本 BSP 目前对外设的支持情况如下：

<th align="left">**板载外设**</th><th align="center">**支持情况**</th><th align="left">**备注**</th>
|------
<td align="left">USB 转串口</td><td align="center">支持</td><td align="left"></td>
<td align="left">SD卡</td><td align="center">支持</td><td align="left"></td>
<td align="left">IRDA</td><td align="center">支持</td><td align="left"></td>
<td align="left">音频接口</td><td align="center">支持</td><td align="left">支持音频输出</td>
<td align="left">**片上外设**</td><td align="center">**支持情况**</td><td align="left">**备注**</td>
<td align="left">GPIO</td><td align="center">支持</td><td align="left">PA PB PE PF</td>
<td align="left">UART</td><td align="center">支持</td><td align="left">UART0/1/2</td>
<td align="left">SDIO</td><td align="center">支持</td><td align="left"></td>
<td align="left">ADC</td><td align="center">支持</td><td align="left">10bit ADC</td>
<td align="left">SPI</td><td align="center">即将支持</td><td align="left">软件 SPI</td>
<td align="left">I2C</td><td align="center">支持</td><td align="left">软件 I2C</td>
<td align="left">RTC</td><td align="center">支持</td><td align="left"></td>
<td align="left">WDT</td><td align="center">支持</td><td align="left"></td>
<td align="left">FLASH</td><td align="center">即将支持</td><td align="left">对接 FAL</td>
<td align="left">TIMER</td><td align="center">支持</td><td align="left"></td>
<td align="left">PWM</td><td align="center">支持</td><td align="left">LPWM 的 G1 G2 G3 之间是互斥的，只能三选一</td>
<td align="left">FM receive</td><td align="center">支持</td><td align="left"></td>
<td align="left">USB Device</td><td align="center">暂不支持</td><td align="left"></td>
<td align="left">USB Host</td><td align="center">暂不支持</td><td align="left"></td>

### 使用说明

使用说明分为如下两个章节：
-  快速上手 本章节是为刚接触 RT-Thread 的新手准备的使用说明，遵循简单的步骤即可将 RT-Thread 操作系统运行在该开发板上，看到实验效果 。 -  进阶使用 本章节是为需要在 RT-Thread 操作系统上使用更多开发板资源的开发者准备的。通过使用 ENV 工具对 BSP 进行配置，可以开启更多板载资源，实现更多高级功能。 
#### 快速上手

本 BSP 为开发者提供 GCC 开发环境。下面介绍如何将系统运行起来。

##### 硬件连接

使用数据线连接开发板到 PC，打开电源开关。

##### 编译下载

通过 `RT-Thread Studio` 或者 `scons` 编译得到 `.dcf` 固件，通过 `Downloader` 进行下载

##### 运行结果

下载程序成功之后，系统会自动运行，观察开发板上 LED 的运行效果，红色 LED 会周期性闪烁。

连接开发板对应串口到 PC , 在终端工具里打开相应的串口（15000-8-1-N），复位设备后，可以看到 RT-Thread 的输出信息:

```
 \ | /
- RT -     Thread Operating System
 / | \     4.0.3 build Dec  9 2020
 2006 - 2020 Copyright by rt-thread team
msh &gt;

```

#### 进阶使用

此 BSP 默认只开启了 GPIO 和 串口0 的功能，如果需使用 SD 卡、Flash 等更多高级功能，需要利用 ENV 工具对BSP 进行配置，步骤如下：
1.  在 bsp 下打开 env 工具。 1.  输入`menuconfig`命令配置工程，配置好之后保存退出。 1.  输入`pkgs --update`命令更新软件包。 1.  输入`scons` 命令重新编译工程。 
### 完整代码下载地址：


