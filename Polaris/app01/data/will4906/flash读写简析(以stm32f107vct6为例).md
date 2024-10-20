
--- 
title:  flash读写简析(以stm32f107vct6为例) 
tags: []
categories: [] 

---
## 概述
- flash作为stm32中的存储物质，使用非常广泛。关于flash的概念什么的网上已经有很多介绍，笔者便不再赘述，分享一篇stm32的。- 相对于很多操作寄存器的例子，笔者这篇着重于用库函数处理。
## 代码设计

### 写入

编写代码的时候实际上非常简单。只需要几个步骤就可以完成写入。
- 解锁  `FLASH_Unlock();`  这一步非常简单。只需要调用上面的解锁函数即可。虽然简单，但是不能省略~- 清除相应的标志位  `FLASH_ClearFlag(FLASH_FLAG_EOP | FLASH_FLAG_BSY | FLASH_FLAG_PGERR | FLASH_FLAG_WRPRTERR);`  笔者于头文件中找到了这几个标志位于是全部清除。同样也是不能省略。<li>擦除扇区 
  <ul><li>这一步是整个写入过程中最为让人不解的。但是只要搞懂了原理。其实也不是那么难懂。 
    <blockquote> 
     flash中有一个叫**扇区**的概念，有的教材也称为**页**。按照不同容量，flash存储器组织成32个1K字节/页(小容量)、 128个1K字节/页(中容量)、 256个2K字节/页(大容量)的主存储器块和一个信息块。 
    </blockquote></li>- st公司提供的擦除flash扇区库函数，一次至少要擦除一个扇区。  `FLASH_Status FLASH_ErasePage(uint32_t Page_Address)`  其中Page_Address是要擦除扇区的地址，若传入的不是首地址也会对齐到首地址擦除相应的一个扇区。也就是说我们存在这个扇区上的所有东西都会被清除。- 如果不清除该扇区，我们是没有办法在该扇区上写东西的。据说这样是因为硬件设计的原因（笔者不是很确定）。- 这里就涉及到了一个可擦除范围的问题。flash的地址范围那么大，会不会有什么地方是不能擦除的呢。答案是有的。经过笔者的实验，笔者的stm32f107vct6的地址范围是0x08032000~0x0803FFC4。至于为什么不是从flash的起始地址0x08000000开始呢。根据笔者的查询，是因为避开rom开始的位置，不能把正在运行的程序给擦除了，至于为什么是在0x0803FFC4结束，这个笔者就不是特别明白了，但是总的来说不影响我们的使用。
写入数据

这也是最关键的一步，前面说了半天，都是为这个做铺垫。

先介绍一个**字**和**半字**的概念

>  
   字(Word)： 32位长的数据或指令 
   半字(Half Word)： 16位长的数据或指令  
  

flash的写入是分字和半字的。

`FLASH_Status FLASH_ProgramHalfWord(uint32_t Address, uint16_t Data)`

`FLASH_Status FLASH_ProgramWord(uint32_t Address, uint32_t Data)`

根据所指定的地址，一次只能写进一个数据。

上锁

最后一步，重新锁定

`FLASH_Lock();`

流程图

### 读取

读取就更为简单了，只需要根据地址转为指针在转为数据即可  `pBuf[i] = *((u16*)startAddr + i);`

### 例程


