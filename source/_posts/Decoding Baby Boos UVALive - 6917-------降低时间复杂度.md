---
title: Decoding Baby Boos UVALive - 6917-------降低时间复杂度
date: 2017-08-04 11:04:58
categories: 数据结构
---
原题传送门 ：https://cn.vjudge.net/problem/UVALive-6917  

题意很简单的一道题，甚至很多大牛都没读题目看了输入输出直接敲，我们出了一个问题，超时三发。这道题罚时太严重。罚时多，过得慢，应该好好思考一下自己队伍的状态

现在总结做法如下：

    
    
    #include <iostream>
    #include <cstring>
<!-- more -->    #include <cmath>
    #include <cstdio>
    #define inf 0x3f3f3f
    using namespace std;
    char s[110000];
    int main ()
    {
        int t;
        scanf("%d",&t);
         getchar();
        while(t--)
        {
            char v[30]= {"ABCDEFGHIJKLMNOPQRSTUVWXYZ"};
            scanf("%s",s);
            int m;
            scanf("%d",&m);
            char a,b;
            while(m--)
            {
                getchar();
                scanf("%c %c",&a,&b);
                for(int i=0; i<26; i++) //根据 样例输入2，就找到这个问题了，
                {
                    if(v[i]==b) 
                     v[i]=a;
                }
            }
             //如果，v的值没有 改变 那么s[i] = v[s[i]-'A']是一定的 如果出现了变化，v【i】也发生了变化，这样就把算法的复杂度降了下来。
             int n=strlen(s);
            for(int i=0; i<n; i++)
            {
                if(s[i]>='A' &&s[i]<='Z')
                    s[i]=v[s[i]-'A'];
            }
            printf("%s\n",s);
    
        }
    }
    

  
  

  

