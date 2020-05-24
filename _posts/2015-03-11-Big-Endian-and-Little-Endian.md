---
layout: post
date: 2015-03-11 15:36:00
title: 大端与小端
tag: [网络]
---

### 高内存地址和低内存地址
内存布局大致如下：

```markup
-----------------------最高内存地址0xffffffff  
栈底  
栈  
栈顶  
-----------------------  
NULL (空洞)  
-----------------------
堆
-----------------------
未初始 化的数据
----------------------- 统称数据段
初始化的数据
-----------------------
正 文段(代码段)
----------------------- 最低内存地址 0x00000000
```

假如有一个4字节的数组 char[4] szBuf; 那么szBuf在内容中的分布如下： 

```markup
栈底 （高地址）
----------
szBuf[3]
szBuf[2]
szBuf[1]
szBuf[0]
----------
栈顶 （低地址）
```

### 高字节和低字节
在十进制中我们都说靠左边的是高位，靠右边的是低位，在其他进制也是如此。  
比如有一个16进制的数： 0x12345678，一共占用4个字节的内存空间，从左到右表示：高字节 --> 低字节，分别是：  
>0x12，0x34，0x56，0x78

在内存中的分布根据大小端的不同，顺序就相反：  
大端：
```markup
栈底 （高地址）
---------------
0x78 -- 低位字节
0x56
0x34
0x12 -- 高位字节
---------------
栈顶 （低地址）
```

小端：
```markup
栈底 （高地址）
---------------
0x12 -- 高位字节
0x34
0x56
0x78 -- 低位字节
--------------
栈 顶 （低地址）
```
### 大端和小端
简单点来说：  
大端：高字节存放在低地址。  
小端：高字节存放在高地址。  
怎么记住呢？可以联想 “负负得正” 来记忆，**高高为小**（*即高地址存放高字节为小端*），这样以后就不怕忘记了。

PS：关于进程在内存（虚拟内存）中的分布情况，请参考我的[读书笔记——《Unix环境高级编程》第7章](http://domicat.me/apue-3rd/)。