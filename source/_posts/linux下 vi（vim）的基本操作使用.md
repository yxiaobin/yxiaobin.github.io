---
title: linux下 vi（vim）的基本操作使用
date: 2018-01-06 19:59:33
categories: linux
---
以目前的我来看，vi就是vim，他们的操作也有着很大的相似性或者说共性。

现在总结操作如下：

vim 一共有三种模式

一般模式，编辑模式，以及命令行模式

1\. 打开文件 操作： vi 文件名 （进入一般模式）

一般模式下，无法插入，只能阅读，移动光标。

一般摸下有如下的操作

![](https://img-
blog.csdn.net/20180106195201457?water<!-- more -->mark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4MDY0ODEw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  

2\. 通过 按键（a i o） 键入到编辑模式，此时可以进行编辑，按Esc 按钮退出到一般模式

3\. 通过： 进入命令行模式， ！代表强制操作 q代表退出 w代表保存

命令行模式下：

/串 将光标定位到该串上， ？串，将光标定位到该穿上，两者操作开始的地方不同一个从上到下，一个从下到上

set number 可以在vim上添加行号

%s/old/new/g 把old 全部替换掉，变成new

其他操作见照片

![](https://img-
blog.csdn.net/20180106195855727?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4MDY0ODEw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![](https://img-
blog.csdn.net/20180106195904442?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4MDY0ODEw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  

  

  

