---
title: Salty Fish---DP的变形
date: 2017-07-24 21:23:48
categories: 数据结构
---
  
  
海边躺着一排咸鱼，一些有梦想的咸鱼成功翻身（然而没有什么卵用），一些则是继续当咸鱼。一个善良的渔夫想要帮这些咸鱼翻身，但是渔夫比较懒，所以只会从某只咸鱼开始，往一个方向，一只只咸鱼翻过去，翻转若干只后就转身离去，深藏功与名。更准确地说，渔夫会选择一个区间[L,R]，改变区间内所有咸鱼的状态，至少翻转一只咸鱼。  
  
渔夫离开后想知道如果他采取最优策略，最多有多少只咸鱼成功翻身，但是<!-- more -->咸鱼大概有十万条，所以这个问题就交给你了！  
Input  
  
包含多组测试数据。  
  
每组测试数据的第一行为正整数n，表示咸鱼的数量。  
  
第二行为长n的01串，0表示没有翻身，1表示成功翻身。  
  
n≤100000  
Output  
  
在渔夫的操作后，成功翻身咸鱼（即1）的最大数量。  
Sample Input  
  
5  
1 0 0 1 0  
3  
0 1 0  
  
Sample Output  
  
4  
2  
  
Hint  
  
对于第一个样例，翻转区间[2,3]，序列变为1 1 1 1 0。  
  

对于第二个样例，翻转整个区间，序列变为1 0 1。

  

思路：

1）首先记录一下初始状态下的1 的个数，然后设一个新数组，1的时候标记为-1,0的时候标记为1，

对这个新数组进行dp，找最大和。

2）如果对于当前a[i]，如果dp[i-1]<0 那么 dp[i]=a[i],如果dp[i-1]>0, 那么 a[i] = dp[i-1] + a[i];

3） 一遍for 循环 把最大的dp[i]找到就可以了。

    
    
    #include<iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int main ()
    {
        int n,i,k;
        int a[110000];
        int dp[110000];
        while(~scanf("%d",&n))
        {
            int sum=0;
            for(i=0;i<n;i++)
            {
                scanf("%d",&k);
                if(k==1)
                {
                    a[i]=-1;
                    sum++;
                }
                else a[i]=1;
            }
            dp[0]=a[0];
            int max=dp[0];
            for(i=1;i<n;i++)
            {
                if(dp[i-1]<0)
                {
                    dp[i]=a[i];
                }
                else
                {
                    dp[i]=a[i]+dp[i-1];
                }
                if(dp[i]>max)
                max=dp[i];
            }
            cout<<max+sum<<endl;
        }
    }
    

  
  

  

