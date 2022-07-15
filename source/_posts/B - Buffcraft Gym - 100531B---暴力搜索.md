---
title: B - Buffcraft Gym - 100531B---暴力搜索
date: 2017-08-15 21:33:11
categories: 数据结构
---
#  传送门：https://cn.vjudge.net/problem/Gym-100531B

  

注意 ：  

对k个状态进行枚举就可以了  

第一组测试样例中的输出顺序是可以换的，没有要求

需要用到 long long

和需要用数组存不然避免超时  

    
    
    #include <cstdio>
    #include <iostream>
    #in<!-- more -->clude <cstring>
    #include <algorithm>
    using namespace std;
    struct node
    {
        int x;
        int id;
    } a[120000], b[120000];//数组需要开的大一点儿
    long long int sum[120000];//第一种直接加的求和
    long long int ans[120000];//第二种百分比的求和
    int cmp ( node a,node b)
    {
        return a.x>b.x;
    }
    double solve(int n, long long int x,long long  int y)// 注意，x y的数据类型 long long
    {
        double k=((n+x)*(100+y)/100.0);
        return k;
    }
    int main ()
    {
        freopen("buffcraft.in", "r", stdin);
        freopen("buffcraft.out", "w", stdout);
        int n,m,x,y;
        scanf("%d %d %d %d",&n,&m,&x,&y);
        for(int i=0; i<x; i++)
        {
            scanf("%d",&a[i].x);
            a[i].id=i+1;
        }
        for(int i=0; i<y; i++)
        {
            scanf("%d",&b[i].x);
            b[i].id=i+1;
        }
        sort(a,a+x,cmp);
        sort(b,b+y,cmp);
        sum[0]=a[0].x;
        ans[0]=b[0].x;
        for(int i=1;i<x;i++)
        {
            sum[i]=sum[i-1]+a[i].x; //存到没一状态的和
        }
        for(int i=1;i<y;i++)
        {
            ans[i]=ans[i-1]+b[i].x;
        }
        int p=0,q=0;
        double M;
        M=0;
        for(int i=0; i<=x; i++)
        {
            if (i>m) break; //注意 如果break ，会多跑很多超时
            int j=m-i;
            if(j>y) j=y; // j>y 并不能取break，因为很可能此时的第一种还可以多取，第二种只不过只能取y种
            long long sum1, sum2;
            if(i==0) sum1=0;
            else  sum1=sum[i-1];
            if(j==0) sum2=0;
            else  sum2=ans[j-1];
            double  Max=solve(n,sum1,sum2);
            if(Max>M)
            {
                M=Max;
                p=i;
                q=j;
            }
        }
        printf("%d %d\n",p,q);
        for(int i=0; i<p; i++)
        {
            printf("%d%c",a[i].id, i==p-1?'\n':' ');
        }
        for(int i=0; i<q; i++)
        {
            printf("%d%c",b[i].id, i==q-1?'\n':' ');
        }
        return 0;
    }
    

  
  

