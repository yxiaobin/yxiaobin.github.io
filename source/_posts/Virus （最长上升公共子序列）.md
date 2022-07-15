---
title: Virus （最长上升公共子序列）
date: 2017-06-10 21:44:16
categories: 数据结构文章标签
---
We have a log le, which is a sequence of recorded events. Naturally, the
timestamps are strictly  
increasing.  
However, it is infected by a virus, so random records are inserted (but the
order of or<!-- more -->iginal events  
is preserved). The backup log le is also infected, but since the virus is
making changes randomly, the  
two logs are now different.  
Given the two infected logs, your task is to nd the longest possible original
log le. Note that there  
might be duplicated timestamps in an infected log, but the original log le
will not have duplicated  
timestamps.  
Input  
The rst line contains  
T  
(  
T  
  
100), the number of test cases. Each of the following lines contains two  
lines, describing the two logs in the same format. Each log starts with an
integer  
n  
(1  
  
n  
  
1000),  
the number of events in the log, which is followed by  
n  
positive integers not greater than 100,000, the  
timestamps of the events, in the same order as they appear in the log.  
Output  
For each test case, print the number of events in the longest possible
original log le.  
Sample Input  
1  
9 1 4 2 6 3 8 5 9 1  
6 2 7 6 3 5 1  
Sample Output  

3

算法 ：ＬＣＩＳ算法

思想 ，可以看成一个二维数组，一个代表行，一个代表列，当ａ数组长度为ｉ，ｂ数组长度为ｊ的时候，他们的最大的数组长度为在ａ【ｉ－１】 和
ｂ【ｊ－１】的前提下，如果 ａ【i】＝ｂ【ｊ】并且ｂ【ｊ】>b[j-1] 的时候，长度为 在上一个长度上 ＋１．

不难想到 三层 ｆｏｒ 循环 下的上述

int a[100], b[100], c[100][100];  
for(i=0;i<n;i++)  
{  
for(j=0;j<m;j++)  
{  
c[i][j]=c[i-1][j-1];  
MAX=0;  
if(a[i]==b[j])  
{  
for(k=0;k<=j-1;k++)  
{  
if(b[j]>b[k] && c[i][k]>MAX)  
{  
MAX=c[i][k];  
}  
}  
c[i][j]=MAX+1;  
}  
}  
}

但是 如你所见，三层循环，可能会有超时的下场。又因为ｋ这层的循环于ｊ这层的循环息息相关，我们是可以把他变成二重循环的

  
int a[100], b[100], c[100][100];  
for(i=0; i<n; i++)  
{  
MAX=0;  
for(j=0; j<m; j++)  
{  
c[i][j]=c[i-1][j-1];  
if(a[i]>b[j] && c[i][j]>MAX) /*仔细琢磨一下为啥可以变成ａ【ｉ】 和 ｂ【ｊ】 进行比较*／  
  
{  
MAX=c[i][j];  
}  
if(a[i]==b[j])  
{  
  
c[i][j]=MAX+1;  
}  
}  
}  
  
再继续看的话，二位数粗c[i][j] ,可以继续变为一维 的，他可以不断的更新，于是就变成了下面的这个代码

int a[100], b[100], c[100];  
for(i=0; i<n; i++)  
{  
MAX=0;  
for(j=0; j<m; j++)  
{  
c[j]=c[j-1];  
if(a[i]>b[j] && c[j]>MAX) /*仔细琢磨一下为啥可以变成ａ【ｉ】 和 ｂ【ｊ】 进行比较*/  
  
{  
MAX=c[j];  
}  
if(a[i]==b[j])  
{  
  
c[j]=MAX+1;  
}  
}  
}  

(思绪可能会有点乱，有些地方没有想好怎么解释，望见谅)  

    
    
    #include <iostream>
    #include <cstring>
    #include <cstdio>
    #include <cmath>
    #include <algorithm>
    using namespace std;
    int a[1500];
    int b[1500];
    int dp[1500];
    
    int main ()
    {
        int n,m,i,j,k,f,t;
        cin >>t;
        while(t--)
        {
             cin >>n;
             for(i=1;i<=n;i++)
             cin >>a[i];
             cin >>m;
             for(i=1;i<=m;i++)
             cin >>b[i];
             memset(dp,0,sizeof(dp));
             for(i=1;i<=n;i++)
             {
                f=0;
                for(j=1;j<=m;j++)
                {
                    if(a[i]>b[j]&& dp[j]>f)
                   {
                      f=dp[j];
                   }
                   if(a[i]==b[j])
                   {
                        dp[j]=f+1;
                   }
                }
             }
             f=0;
             for(i=1;i<=m;i++)
             {
                if(dp[i]>f)
                {
                    f=dp[i];
                }
             }
             cout<<f<<endl;
        }
    }
    
    
    

  
  

  
  
  

