---
title: F——quadratic equation
date: 2017-05-11 22:51:26
categories: 数据结构文章标签
---
###  quadratic equation

Time Limit: 2000MS  Memory Limit: 131072KB

[ Submit
](http://acm.sdut.edu.cn/onlinejudge2/index.php/Home/Contest/contestsubmit/cid/2164/pid/3898.html)
[ Statistic
](http://ac<!-- more -->m.sdut.edu.cn/onlinejudge2/index.php/Home/Contest/conteststatus/cid/2164/pid/3898.html)

####  Problem Description

With given integers  a  ,  b  ,  c  , you are asked to judge whether the
following statement is true: "For any  x  , if  a  ⋅
![](http://acm.sdut.edu.cn/image/3898.png) \+  b  ⋅  x  \+  c  =0, then  x  is
an integer."

####  Input

The first line contains only one integer  T  (1≤  T  ≤2000), which indicates
the number of test cases.  
For each test case, there is only one line containing three integers  a  ,  b
,  c  (−5≤  a  ,  b  ,  c  ≤5).

####  Output

or each test case, output “ ` YES ` ” if the statement is true, or “ ` NO ` ”
if not.

####  Example Input

    
    
    3
    1 4 4
    0 0 1
    1 3 1
    

####  Example Output

    
    
    YES
    YES
    NO

提示：

1.题目要求一定要读懂： 对于满足ax*x+b*x+c=0 的解x 一定是整数解。

2\. 由第二组样例可以知道 无解的情况 下输出YES

3\. 不要考虑复数域的解集，省赛的时候有很多大佬都想到了这点莫名掉坑。

4\. 不要忽略 有无解 ，abc等于0的情况特别是 0 0 0 此时x的解是实数R应该输出NO。

我的解法：

根据题目，可以知道abc的范围是-5到5 大约估计一下 他的解肯定在-1000 到1000
中，我让他从这个范围遍历一遍，看有几个跟满足此方程。如果代尔特大于0那么应该有两个，如果代尔特等于0那么应该有一个，在考虑一下特殊情况 就好了。

    
    
    #include<stdio.h>
    #include <math.h>
    int main ()
    {
    int a,b,c,i,j,t,sum;
    scanf("%d",&t);
    while (t--)
    {
    scanf("%d %d %d",&a,&b,&c);
    if(a==0)
    {
    sum=0;
    if(b==0)
    {
    if(c!=0) printf("YES\n");
    else printf("NO\n");
    }
    else
    {
    
    for(i=-1000; i<=1000; i++)
    {
    if(b*i+c==0)
    {
    sum++;
    }
    }
    if(sum==1)
    {
    printf("YES\n");
    }
    else
    {
    printf("NO\n");
    }
    
    }
    }
    if(a!=0)
    {
    sum=0;
    j=(b*b)-(4*a*c);
    if(j<0 ) printf("YES\n");
    else
    {
    for(i=-1000; i<=1000; i++)
    {
    if( (a*i*i)+(b*i)+c==0)
    {
    sum++;
    }
    }
    if( (sum==1 &&j==0 ) || (sum==2 && j>0 ) )
    {
    printf("YES\n");
    }
    else
    {
    printf("NO\n");
    }
    }
    }
    
    }
    return 0;
    
    }

  
  

  

