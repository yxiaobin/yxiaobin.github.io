---
title: Piggy-Bank HDU - 1114 －－－完全背包模板
date: 2017-08-07 21:08:42
categories: 数据结构文章标签
---
#  传送门：http://acm.hdu.edu.cn/showproblem.php?pid=1114

完全背包，每个物品都有无限个，可以进行多次的取用  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <!-- more --><map>
    #define inf 999999
    using namespace std;
    int main ()
    {
        int pi[12000];
        int wi[12000];
        int dp[12000];
        int n,m,t;
        scanf("%d",&t);
        while (t--)
        {
            scanf("%d %d",&n,&m);
            for(int i=0; i<m;i++)
            {
                dp[i]=999999;
            }
            int ans=m-n;
            int x;
            scanf("%d",&x);
            for(int i=0; i<x; i++)
                scanf("%d %d",&pi[i], &wi[i]);
            dp[0]=0;
            for(int i=0; i<x; i++)
            {
                for(int j=wi[i]; j<=ans; j++)
                {
                    dp[j]=min(dp[j],dp[j-wi[i]]+pi[i]);
                }
            }
            if(dp[ans]==999999) printf("This is impossible.\n");
            else  printf("The minimum amount of money in the piggy-bank is %d.\n",dp[ans]);
        }
    }
    

  
  

