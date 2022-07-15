---
title: C_fireworks
date: 2017-05-15 17:17:36
categories: 数据结构文章标签
---
###  fireworks

Time Limit: 1000MS  Memory Limit: 65536KB

####  Problem Description

Hmz likes to play fireworks, especially when they are put regularly.  
Now he puts some fireworks in a line. This <!-- more -->time he put a trigger on each
firework. With that trigger, each firework will explode and split into two
parts per second, which means if a firework is currently in position  x  ,
then in next second one part will be in position  x  −1 and one in  x  +1.
They can continue spliting without limits, as Hmz likes.  
Now there are  n  fireworks on the number axis. Hmz wants to know after  T
seconds, how many fireworks are there in position  w  ?

![](http://acm.sdut.edu.cn/image/3895.png)

####  Input

Input contains multiple test cases.  
For each test case:

  * The first line contains 3 integers  n  ,  T  ,  w  (  n  ,  T  ,|  w  |≤10^5) 
  * In next  n  lines, each line contains two integers  xi  and  ci  , indicating there are  ci  fireworks in position  xi  at the beginning(  ci  ,|  xi  |≤10^5). 

####  Output

For each test case, you should output the answer MOD 1000000007.

####  Example Input

    
    
    1 2 0
    2 2
    2 2 2
    0 3
    1 2
    

####  Example Output

    
    
    2
    3
    
    
    提示：很容易看出来这是一个杨辉三角的变形但是数量级为10^5次方 数据量太大不可能之解用二维数组之解存储，我们知道杨辉三角和组合数是
    
    
    有关系的于是这道题目就变成了寻找组合数里面的 c（n,m) ,手写之后 你会找到 n=t， m=t-x。
    
    
    就下来即使 大组合数的取模了，这里请自行百度一下 路斯卡定理（大组合数取模）的相关知识就能解决了
    
    
    #include <stdio.h>
    #include <algorithm>
    #include <string.h>
    #include <math.h>
    using namespace std;
    const long long mod = 1e9+7;
    const int maxn = 1e5+10;
    typedef long long LL;
    LL fac[maxn];
    LL modxp(LL a,LL b)
    {
        LL res = 1;
        while(b)
        {
            if(b&1)
                res = (res*a)%mod;
            b = b>>1;
            a = (a*a)%mod;
        }
        return res;
    }
    void Init()
    {
        fac[0] = 1;
        for(int i = 1; i < maxn; i++)
        {
            fac[i] = (fac[i-1]*i)%mod;
        }
    }
    LL C(LL a,LL k)
    {
        LL re = 1;
        while(a && k)
        {
            LL aa = a%mod;
            LL bb = k%mod;
            if(aa<bb)
                return 0;
            re = re*fac[aa]*modxp(fac[bb]*fac[aa-bb]%mod,mod-2)%mod;
            a /= mod;
            k /= mod;
        }
        return re;
    }
    int csgo(int x,int t,int w)
    {
        int j;
        int ans=x-t; //杨辉三角的每一行的第一个位置坐标
        int end1=x+t;
        j=(w-ans)%2; //判断 w 是 在 杨辉三角这一行里面的数值是否为0
        if (j==0 && w>=ans && w<= end1)
        {
            int  k=(w-ans)/2;
            C(t,k); //n m 已经找到了 ，只需要利用大组合数模板来求解
        }
        else
        {
            return 0;
        }
    
    }
    int main ()
    {
        long long int n,t,w,a,b,i;
        Init();
        while (~scanf("%lld %lld %lld",&n,&t,&w))
        {
            long long int sum=0;
            for(i=0; i<n; i++)
            {
                scanf("%lld %lld",&a,&b);
    
                    sum += b*csgo(a,t,w)%mod; //n m 已经找到了 ，只需要利用大组合数模板来求解
                    sum=sum%mod;
            }
            printf("%lld\n",sum);
        }
        return 0;
    }
    

  
  

