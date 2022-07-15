---
title: Treats for the Cows---区间dp--逆序推
date: 2017-08-09 21:30:10
categories: 数据结构
---
Description  
FJ has purchased N (1 <= N <= 2000) yummy treats for the cows who get money
for giving vast amounts of milk. FJ sells one treat per day and wants to
maximize the money he receives over a<!-- more --> given period time.  
  
The treats are interesting for many reasons:  
  
The treats are numbered 1..N and stored sequentially in single file in a long
box that is open at both ends. On any day, FJ can retrieve one treat from
either end of his stash of treats.  
Like fine wines and delicious cheeses, the treats improve with age and command
greater prices.  
The treats are not uniform: some are better and have higher intrinsic value.
Treat i has value v(i) (1 <= v(i) <= 1000).  
Cows pay more for treats that have aged longer: a cow will pay v(i)*a for a
treat of age a.  
  
Given the values v(i) of each of the treats lined up in order of the index i
in their box, what is the greatest value FJ can receive for them if he orders
their sale optimally?  
  
The first treat is sold on day 1 and has age a=1. Each subsequent day
increases the age by 1.  
  
Input  
Line 1: A single integer, N  
  
Lines 2..N+1: Line i+1 contains the value of treat v(i)  
  
Output  
Line 1: The maximum revenue FJ can achieve by selling the treats  
  
Sample Input  
  
5  
1  
3  
1  
5  
2  
  
Sample Output  
  
43  
  
Hint  
Explanation of the sample:  
  
Five treats. On the first day FJ can sell either treat #1 (value 1) or treat
#5 (value 2).  
  
FJ sells the treats (values 1, 3, 1, 5, 2) in the following order of indices:
1, 5, 2, 3, 4, making 1x1 + 2x2 + 3x3 + 4x1 + 5x5 = 43.  
  
Source  

USACO 2006 February Gold & Silver

  

思路：区间dp，从后往前面扫，挨着扫一遍，找到最大值

设dp[i][j] 为 取i到j后 的最大值-----（区间dp）

转移方程：dp[i][j]=max(dp[i+1][j]+p[i]*(n+i-j),dp[i][j-1]+p[j]*(n+i-j));
其中n+i-j是第几次

解释方程：

首先明确dp[i][j]的意义，是从i到j的最大值。 变成这样的情况有两种：

1\. 从i+1 到 j ， 加上 a[i]*x  

2\. 从 i 到 j-1 , 加上 a[j]*x

上述两种情况，都可以到dp[i][j]的状况。  

    
    
    #include<iostream>
    #include<cstring>
    #include<cstdio>
    #include<cmath>
    #include<algorithm>
    using namespace std;
    
    int dp[2005][2005];
    int a[2005];
    int main()
    {
        int n;
        while(~scanf("%d",&n))
        {
            memset(dp,0,sizeof(dp));
            for (int i = 1; i<=n; i++)
            {
                scanf("%d",&a[i]);
            }
            for (int i = 1; i<=n; i++)
                dp[i][i] = a[i]*n; //讲对角线进行初始化
            for (int i = n; i>= 1; i--)
            {
                for (int j = i; j<=n; j++)
                {
                    dp[i][j] = max(dp[i+1][j]+(n-j+i)*a[i],dp[i][j-1]+(n-j+i)*a[j]);
                }
            }
            printf("%d\n",dp[1][n]);
        }
    }
    

  

  
  

