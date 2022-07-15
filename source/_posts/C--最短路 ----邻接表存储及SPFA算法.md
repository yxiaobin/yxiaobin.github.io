---
title: C--最短路 ----邻接表存储及SPFA算法
date: 2017-08-01 10:23:57
categories: 数据结构
---
C--最短路  
Time Limit: 7000MS Memory Limit: 65536KB  
Problem Description  
给出一个带权无向图，包含n个点，m条边。求出s，e的最短路。保证最短路存在。  
Input  
多组输入。  
对于每组数据。  
第一行输入n，m(1<= n && n<=5*10^5,1 <= m && m <= 2*10^6)。  
接下来m行<!-- more -->，每行三个整数，u,v,w,表示u，v之间有一条权值为w(w >= 0)的边。  
最后输入s，e。  
Output  
对于每组数据输出一个整数代表答案。  
Example Input  

3 1  
1 2 3  
1 2  

Example Output  

3  

思路：

由于节点的数据范围过大，因此无法利用二维数组存储路径，此时需要使用连接表存储路径。

SPFA算法：  

1.可以解决有负权值的情况。

2.利用队列进行松弛操作。  


​    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    #include <queue>
    #include <vector>
    #define inf 0x3f3f3f3f
    using namespace std;
    struct node
    {
        int id;
        int wi;
    } a,b;
    vector<node>v[500100];
    int vis[500100],dist[500100], n, m;
    void SPFA(int s, int e)
    {
        memset(dist,inf,sizeof(dist));
        memset(vis,0,sizeof(vis));
        dist[s]=0;
        vis[s]=1;
        queue<int>q;
        q.push(s);
        while(!q.empty())
        {
            int x=q.front();
            q.pop();
            vis[x]=0; //大坑点，因为这一句，卡一道题卡了好久好久！！！！
            for(int i=0; i<v[x].size(); i++)
            {
                int id=v[x][i].id;
                int wi=v[x][i].wi;
                if(dist[id] >dist[x]+wi) // 不断进行实时更新保证每一步的 dist 都是最短情况
                {
                    dist[id]=dist[x]+wi;
                    if(!vis[id])
                    {
                        q.push(id);
                        vis[id]=1;
                    }
                }
            }
        }
        cout<<dist[e]<<endl;
    }
    int main ()
    {
        int u,V,w;
        while(~scanf("%d %d",&n,&m))
        {
            for(int i=0; i<m; i++)
            {
                scanf("%d %d %d",&u,&V,&w);
                a.id=V;
                a.wi=w;
                v[u].push_back(a);
                b.id=u;
                b.wi=w;
                v[V].push_back(b);
            }
            int s,e;
            cin >>s>>e;
            SPFA(s,e);
        }
    }




