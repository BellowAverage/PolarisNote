
--- 
title:  [Linux] ps命令详解 
tags: []
categories: [] 

---
## ps命令

ps命令用于显示当前系统中的进程状态信息。以下是ps命令的一些常见参数及其作用：
<li> ps命令的基本形式： <pre><code>ps
</code></pre> 这将显示当前用户自己的运行中的进程的快照。 </li>1.  参数选项： -a: 显示所有进程，包括其他用户的进程。 -u: 显示与用户相关的详细输出。 -x: 显示没有控制终端的进程。 -e: 显示所有进程，同`-A`。 -f: 显示完整格式的输出。 -l: 显示长格式的输出。 <li> 示例输出： <pre><code>$ ps -aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 225600 15568 ?        Ss   Dec11   0:04 /sbin/init splash
root         2  0.0  0.0      0     0 ?        S    Dec11   0:00 [kthreadd]
root         3  0.0  0.0      0     0 ?        I&lt;   Dec11   0:00 [rcu_gp]
...
</code></pre> </li>
在示例输出中，每一列代表的含义如下：
- USER：进程所属用户；- PID：进程ID；- %CPU：进程占用CPU的使用百分比；- %MEM：进程占用物理内存的使用百分比；- VSZ：进程使用的虚拟内存大小（单位为KB）；- RSS：进程占用的实际物理内存大小（单位为KB）；- TTY：进程所属的终端设备，如果没有则显示`?`；- STAT：进程状态，常见的有`S`（休眠）, `R`（运行）, `T`（停止）；- START：进程启动时间；- TIME：进程占用CPU的累计时间；- COMMAND：进程命令名。
### TIME列

TIME列显示的是该进程已经运行的时间。它包含两个值，分别是CPU时间（CPU time）和墙钟时间（Wall clock time）。
-  CPU时间 指的是进程在CPU上实际执行的时间。它包括该进程使用用户态CPU的时间（User Time）和系统态CPU的时间（System Time）。用户态CPU时间是进程在用户空间执行代码的时间，而系统态CPU时间是进程在内核空间执行系统调用和处理中断的时间。这两个时间加在一起就是CPU时间。 -  墙钟时间 是指进程从启动到现在所经过的时间，也称为实际时间。它是指进程在真实世界中运行的时间，包括了进程在运行过程中的等待时间、阻塞时间等。 
在ps aux命令的输出中，TIME列显示的是CPU时间，以[天-小时:分钟:秒]的格式表示。 例如，如果一个进程的TIME值为01-10:30:45， 表示该进程已经在CPU上执行了1天、10小时、30分钟和45秒。

需要注意的是，TIME列并不是实时更新的，它只显示进程启动后的CPU时间。如果进程启动后没有实际执行任何代码，TIME值可能会很小或者为0。
