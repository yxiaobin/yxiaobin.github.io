---
title: Gcc的用法
date: 2018-01-07 20:02:08
categories: linux
---
GCC的简单命令

GCC  的相关命令：

1)  gcc –o  命名  001.c

2)  gcc -E 001.c  预处理

3)  gcc -S 001.c  汇编

4)  gcc -c 001.c  编译

5)  gcc -g 001.c –o out  调试

gdb out

几个一般操作：

run  运行

b  数  跳到第几行

p  参数  打印参数

n  下一<!-- more -->步

6)  gcc -Wall001.c  查看代码警告

7)  gcc –O001.c  优化算法

8)  ldd out  查看链接，  gcc  库依赖

9)  time ./out  可以查看代码运行时间

