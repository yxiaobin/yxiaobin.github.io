---
title: 利用终端进行GDB调试
date: 2018-01-08 19:56:56
categories: linux
---
众所周知，调试的办法有 折半插断点输出的方式，还有局部注释编译运行的方式之外，就是GDB调试了

现总结GDB调试中常用的语句操作。

首选，利用终端编译文件的时候，需要使用选择项 -g 编译可执行文件，不然的花，无法进行GDB调试

GDB的基本语句

命令：  
list  显示局部代码  
b 行号  在第几行插入断点  
b 函数名  在此处插入断点  
b 另一个文件名 行号  在此处插<!-- more -->入断电  
info break  查看断点信息  
run  运行  
n  下一行  
p 变量  查看变量的值  
continue  跳到下一个断点  
q  退出，终止调试  
step  进入到函数里面  
delete  删除所有断点  
clean  删除当前断点  

linux系统下运行程序，会有一个经常遇到的问题---段错误 利用GDB调试寻找段错误的方法

首先了解一下造成段错误的原因：

1.指针没有申请空间却赋值  
2.访问了系统保护的内存地址 int *p = (int *)0  
3.访问只读的内存地址  
4.栈溢出  
·查找段错误的原因

1.在终端中输入 ulimit -c 1024 （开出1024空间抓取段错误）

2\. gdb ./debug ./core.xxxx

3\. bt  打印段错误,找到出错的在第几行

附上一个样例

![](https://img-
blog.csdn.net/20180108195641397?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4MDY0ODEw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  

