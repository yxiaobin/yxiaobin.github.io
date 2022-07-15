---
title: Funny Car Racing UVA - 12661 --SPFA最短路变形
date: 2017-08-01 11:00:17
categories: 数据结构文章标签
---
传送门 ：https://cn.vjudge.net/problem/UVA-12661

思路：

这道题与普通的SPFA最短路不同在于每一条路都有一个开门时间一个关门时间，

这样话，我们只需要判断一下在到某一条路的时候，如果门是关着的，那就等他下一次开门的时候在走，

如果是开着的，如果加上通过的时间依旧没有关，俺就直接过去就好了，如果加上通过的时间，门已经关了，那就等他下一次打开的时候

<!-- more -->走这条路，把等待的时间加上去就好了

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <queue>
    #include <vector>
    #include <algorithm>
    #define inf 0x3f3f3f3f
    using namespace std;
    int n,m,s,t;
    int tt;
    struct node
    {
        int id;
        int x;
        int y;
        int z;
    } a;
    vector<struct node> V[150000];
    long long  int dis[150000];
    int vis[150000];
    //
    void spfa()
    {
        memset(vis,0,sizeof(vis));
        memset(dis,inf,sizeof(dis));
        dis[s]=0;
        vis[s]=1;
        queue<int>q;
        q.push(s);
        while(!q.empty())
        {
            int len=q.front();
            q.pop();
            vis[len]=0;
            for(int i=0; i<V[len].size(); i++)
            {
                int x=V[len][i].x;
                int y=V[len][i].y;
                int z=V[len][i].z;
                int id=V[len][i].id;
                int sum=dis[len] %  (x+y);//
                int w=0;
                if(sum<=x-z)
                w=z;
                else
                {
                    w=z+(x+y-sum);
                }
                if(dis[len]+w<dis[id]  )
                {
                    dis[id]=dis[len]+w;
                    if(!vis[id])
                    {
                          vis[id]=1;
                        q.push(id);
                    }
                }
            }
        }
        cout<<"Case "<<tt++<<": "<<dis[t]<<endl;
    }
    
    int main ()
    {
        int v,u,x,y,z;
        tt=1;
        while(cin>>n>>m>>s>>t)
        {
            for(int i=0; i<=n+1; i++)
                V[i].clear();
            for(int i=0; i<m; i++)
            {
                cin>>u>>v>>x>>y>>z;
    
                if(x>=z)
                {
                    a.id=v;
                    a.x=x;
                    a.y=y;
                    a.z=z;
                    V[u].push_back(a);
                }
            }
            spfa();
        }
    
      return 0;
    }
    

  
  

