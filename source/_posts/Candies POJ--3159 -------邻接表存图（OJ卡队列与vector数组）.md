---
title: Candies POJ--3159 -------邻接表存图（OJ卡队列与vector数组）
date: 2017-08-04 20:49:03
categories: 数据结构
---
#  传送门：http://poj.org/problem?id=3159

这道题很不友好！！！卡掉了queue，卡掉了vector，这么卡题，像我一样的弱儿怎么办啊！！！！！！！！

于是，乖乖的百度---“图的邻接表存储方式”，啊啊啊，本以为vector 可以用到死的啊！！！

分割线

\---------------------------------------------------<!-- more -->----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------这道题的意思是
分糖果 ，输入 abc，意思是a同学觉得b同学顶多比他多c个糖果，问满足条件下的1到n的最大差值，本来就是一个英文题，读出这个题意来满脸懵逼？？？

这是最短路专题的题？？懵逼了一会儿，这题怎么办，既然是最短路专题啊，那就往最短路上想啊，那路径呢，点呢？ 找啊～～那么 a到 b
点的路径就是c啊，于是乎，我们就找到了所有点，与所有点之间的路径值了，满足分糖果的要求的，并且求n与1差的最大值，如果 有输入 a c 6 ，a b 2，
b c 3；这么三组数据，按照这个专题(这个专题，裸的最短路真的太少了…………哭)的尿性，不是找最短路就是找最长的路，假设找最长的路，设a的值为1 跟据
ac6 那么c的值便是7 b的值便是3 此时c比b大4 ，不满足条件，最长路否定。假设找最短路此时
ac应该为5，同样设a为1那么c的值就是6了，b为3，此时满足 bc3 的要求。通过这个蛋疼的特例分析，这是一道最短路问题。

由于n的范围太大，于是，我就利用了vector，超时，用了队列超时…………

用队列超时怎么办，栈来凑，道理一个样的！！

vector超时怎么办，数组建临接表

代码送上

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    #include <vector>
    #include <stack>
    #include <queue>
    #define inf 0x3f3f3f3f
    using namespace std;
    struct nood
    {
        int u;
        int id;
        int next;
        int wi;
    }edge[40200];
    int head[40200];
    int vis[40200];
    int dist[40200];
    int m,n,cnt;
    void add_edge(int x, int y, int z)
    {
        edge[cnt].id=y;
        edge[cnt].wi=z;
        edge[cnt].next=head[x];
        head[x]=cnt++;
    }
    void SPFA()
    {
        memset(vis,0,sizeof(vis));
        memset(dist,inf,sizeof(dist));
        dist[1]=0;
        stack<int>q;
        q.push(1);
        while(!q.empty())
        {
            int b=q.top();
            q.pop();
            vis[b]=0;
            for(int i=head[b];~i;i=edge[i].next)
            {
                int id=edge[i].id;
                int wi=edge[i].wi;
                if(dist[id]>dist[b]+wi)
                {
                    dist[id]=dist[b]+wi;
                    if(!vis[id])
                    {
                        vis[id]=1;
                        q.push(id);
                    }
                }
            }
        }
        cout<<dist[n]<<endl;
    }
    int main ()
    {
        int x,y,z;
        while (~scanf("%d %d",&n,&m))
        {
            cnt=0;
             memset(head,-1,sizeof(head));
            for(int i=0;i<m;i++)
            {
                scanf("%d %d %d",&x,&y,&z);
                add_edge(x,y,z);
            }
            SPFA();
        }
        return 0;
    }
    

  
  

