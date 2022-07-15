---
title: makefile 的 基本使用
date: 2018-01-08 19:45:15
categories: linux
---
make 工具

makefile是如何工作的：

![](https://img-
blog.csdn.net/20180108194320918?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4MDY0ODEw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gr<!-- more -->avity/SouthEast)  

1.makefile 基本由 目标 依赖 命令 三部分组成的规则

2.基本格式为 ：

目标：依赖文件

Tab + 命令1

Tab + 命令2  

……

3.makefile中可以使用变量，如果存在 定义 SOURCE = main.c

可以采用 $(SOURCE) 的方式来进行调用

4.makefile中 cd命令只能够影响命令行的这以行语句

5.如果命令太长，可以用\换行续写，但是\后面不能在跟任何字符，只可以跟回车

6.makefile 中还存在两个动作 他们为 clean 和 Install 命令，不需要依赖关系，只是需要在后面

Tab + 命令即可

7.后缀规则

.c.o：

gcc -c $< (作用，是把.c的文件全部升成.o)

8.makefile 生成单个可执行文件之后就会结束，因此如果要想生成多个可执行文件，需要建立一个all关系，给

所有的可执行文件建立一个依赖关系

  

  

