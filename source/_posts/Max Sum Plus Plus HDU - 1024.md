---
title: Max Sum Plus Plus HDU - 1024
date: 2017-08-09 15:54:34
categories: 数据结构
---
Problem Description  
Now I think you have got an AC in Ignatius.L's "Max Sum" problem. To be a
brave ACMer, we always challenge ourselves to more difficult problems. Now you
are faced with a more dif<!-- more -->ficult problem.  
  
Given a consecutive number sequence S1, S2, S3, S4 ... Sx, ... Sn (1 ≤ x ≤ n ≤
1,000,000, -32768 ≤ Sx ≤ 32767). We define a function sum(i, j) = Si + ... +
Sj (1 ≤ i ≤ j ≤ n).  
  
Now given an integer m (m > 0), your task is to find m pairs of i and j which
make sum(i1, j1) + sum(i2, j2) + sum(i3, j3) + ... + sum(im, jm) maximal (ix ≤
iy ≤ jx or ix ≤ jy ≤ jx is not allowed).  
  
But I`m lazy, I don't want to write a special-judge module, so you don't have
to output m pairs of i and j, just output the maximal summation of sum(ix,
jx)(1 ≤ x ≤ m) instead. ^_^  
  
  
Input  
Each test case will begin with two integers m and n, followed by n integers
S1, S2, S3 ... Sn.  
Process to the end of file.  
  
  
Output  
Output the maximal summation described above in one line.  
  
  
Sample Input  
  
1 3 1 2 3  
2 6 -1 4 -2 3 -2 3  
  
  
  
Sample Output  
  
6  
8  
  
Hint  
  

Huge input, scanf and dynamic programming is recommended.

  

思路：  

> dp[i][j]表示前j个数分为i部分的最大和，
>
> dp[i][j] = max(dp[i][j-1] + a[j], dp[i-1][k] + a[j]) i-1<=k<=j-1  
>  前者是将第j个数加入到第i部分，后者是将第j个数做为第i部分的第一个数。
>
> ####  因为题目n值范围过大，显然二维数组不行。  
>
>
>   1. 而d[i][x]只与d[i-1][x]有关，所以可以将其降低至一维。  
>  即dp[j]表示前j个数所分段后的和。
>   2. 因为dp[i-1][k]的取值需要一重循环，极有可能导致超时，所以使用数组max存储当前层的最大值，以供下一层求值使用。  
>  dp[j] = max(dp[j-1] + a[j], max[j-1] + a[j])
>

>  
>  
>     #include <iostream>
>     #include <cstdio>
>     #include <cstring>
>     #define inf 0x3f3f3f3f
>     using namespace std;
>     int a[1000100];
>     int b[1000100];//用来记录前一次状态的最优解，避免dp开二维数组
>     int dp[1000100];
>     int main ()
>     {
>        int n,m,M;
>         while(~scanf("%d %d",&m,&n))
>         {
>             for(int i=1; i<=n; i++)
>             {
>                 scanf("%d",&a[i]);
>             }
>             memset(b,0,sizeof(b));
>             memset(dp,0,sizeof(dp));
>             dp[0]=0;
>             b[0]=0;
>             for(int i=1; i<=m; i++)
>             {
>                 M=-inf;
>                 for(int j=i; j<=n; j++)
>                 {
>                     dp[j]=max(dp[j-1]+a[j],b[j-1]+a[j]);
>                     b[j-1]=M;//记录前一个最优值
>                     M=max(M,dp[j]);
>                 }
>             }
>            //printf("%d\n",M);
>            cout<<M<<endl;
>         }
>         return 0;
>     }
>  
>
>  
>  
>
>
>  
>

  

