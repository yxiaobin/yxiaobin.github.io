---
title: Cow Hurdles POJ-3615-------没想到不会TLE的Floyd算法
date: 2017-08-05 19:31:52
categories: 数据结构
---
#  传送门：http://poj.org/problem?id=3615

一下午两个小时，最小生成树，地杰斯特拉，堆优化，24发各种tle，wa
到怀疑人生………………没想到，用到了，最暴力的三重for循环版本额floyd算法！！！

不过，赛后想一想，这个三重循环跑一边就可以把所有的情况全部记住了，如果用上述两种算法，需要跑t次，t最多为4w，需要跑4w次，确实上面的这个算法快，

平时训练<!-- more -->的时候由于这个算法太暴力了，基本不用。这次训练赛也算是吃到了教训吧，以后加油

  

Floyd算法 三重for循环需要主要一点：

中间变量k，要放在for循环的第一层

代码如下：

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <queue>
    #include <algorithm>
    #include <vector>
    #define inf 0x3f3f3f3f
    using namespace std;
    int n,m,t;
    int map[1200][1200];
    int vis[1200];
    int dist[1200];
    void Floyd()
    {
        for(int k=1;k<=n;k++)
        {
            for(int i=1;i<=n;i++)
            {
                for(int j=1 ;j<=n;j++)
                {
                    int Max=max(map[i][k], map[k][j]);
                    map[i][j]=min(map[i][j],Max);
                }
            }
        }
    }
    int main ()
    {
        int x,y,z;
        scanf("%d %d %d",&n,&m,&t);
        memset(map,inf,sizeof(map));
        for(int i=0; i<m; i++)
        {
            scanf("%d %d %d",&x,&y,&z);
            if(map[x][y]>z)
            {
                map[x][y]=z;
            }
        }
        Floyd();
        int ans;
        for(int i=0; i<t; i++)
        {
            ans=inf;
            scanf("%d %d",&x,&y);
            ans=map[x][y];
            if(ans==inf) printf("-1\n");
            else printf("%d\n",ans);
        }
        return 0;
    }
    
    

  
  

