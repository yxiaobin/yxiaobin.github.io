---
title: Hanol towers [Gym-101243B]———Python语言在编程中的文件读入与输出，例题解释
date: 2017-08-24 21:26:29
categories: Python
---
#  传送门：https://cn.vjudge.net/problem/Gym-101243B

汉诺塔，根据题目中给的程序，进行打表，寻找一下，三个柱子上盘子相同时一共需要几步操作

num【3】= 2，num【6】=9，num【12】=38

当 i 为奇数的时候：num【i】=num【i-3】*4+2

当 i 为偶数的时候：num【i】=num【i-3】*4 - t【i】

其中 t【i<!-- more -->】=t【i-6】*4+21

然后，，python 大法好……

  

    
    
    f = open("INPUT.TXT","r")
    p = open("OUTPUT.TXT", "w")
    n = int(f.read())
    a=n/3
    if a%2==0 :
    	p.write(str(int(2**(2*n/3-1)-1+2**(n/3-1)-1+1)))
    else :	
    	n=n-3
    	p.write(str(int(2**(n*2/3-1)-1+2**(n/3-1)-1+1)*4+2))	
    	

  
  

