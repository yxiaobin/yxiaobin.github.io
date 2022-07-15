---
title: D - Digits Gym - 100531D-----暴力搜索
date: 2017-08-15 19:47:01
categories: 数据结构
---
#  传送门 ：https://cn.vjudge.net/problem/Gym-100531D

  

明明是一道水题，却局限于思维定式出不来，应该好好思考一下！！

数据范围只有5000， 暴力搜到100000，就可以了，一秒完全可以！！！

    
    
    #include <cstdio>
    #include <iostream>
    #include <cstr<!-- more -->ing>
    #include <algorithm>
    using namespace std;
    long long int a[5500000];
    long long int num[550000];
    long long int sum[550000];
    long long int get_sum(long long int x)
    {
        long long int sum=0;
        while(x)
        {
            sum+=x%10;
            x/=10;
        }
        return sum;
    }
    void Init()
    {
        long long int i,t;
        for(i=1; i<=100000; i++)
        {
            t=get_sum(i);//表示各位之和
            num[t]++; // 当前和下的个数为多少
            sum[t]+=i;// 当前和下的实际数字和
            //数字a表示当前个数下他的实际数字和的最小值
            if(a[num[t]]==0) a[num[t]]=sum[t];
            else a[num[t]]=min(a[num[t]],sum[t]);
        }
    }
    int main ()
    {
        freopen("digits.in", "r", stdin);
        freopen("digits.out", "w", stdout);
    
        Init();
        long long int n;
        while (~scanf("%lld",&n))
        {
            printf("%lld\n",a[n]);
        }
        return 0;
    }
    

  
  

