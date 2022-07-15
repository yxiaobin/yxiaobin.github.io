---
title: F - Wormholes POJ - 3259--SPFA 算法判断负环是否存在
date: 2017-08-02 15:58:11
categories: 数据结构
---
  
  
While exploring his many farms, Farmer John has discovered a number of amazing
wormholes. A wormhole is very peculiar because it is a one-way path that
delivers you to its destination at a time <!-- more -->that is BEFORE you entered the
wormhole! Each of FJ's farms comprises N (1 ≤ N ≤ 500) fields conveniently
numbered 1..N, M (1 ≤ M ≤ 2500) paths, and W (1 ≤ W ≤ 200) wormholes.  
  
As FJ is an avid time-traveling fan, he wants to do the following: start at
some field, travel through some paths and wormholes, and return to the
starting field a time before his initial departure. Perhaps he will be able to
meet himself :) .  
  
To help FJ find out whether this is possible or not, he will supply you with
complete maps to F (1 ≤ F ≤ 5) of his farms. No paths will take longer than
10,000 seconds to travel and no wormhole can bring FJ back in time by more
than 10,000 seconds.  
Input  
Line 1: A single integer, F. F farm descriptions follow.  
Line 1 of each farm: Three space-separated integers respectively: N, M, and W  
Lines 2.. M+1 of each farm: Three space-separated numbers ( S, E, T) that
describe, respectively: a bidirectional path between S and E that requires T
seconds to traverse. Two fields might be connected by more than one path.  
Lines M+2.. M+ W+1 of each farm: Three space-separated numbers ( S, E, T) that
describe, respectively: A one way path from S to E that also moves the
traveler back T seconds.  
Output  
Lines 1.. F: For each farm, output "YES" if FJ can achieve his goal, otherwise
output "NO" (do not include the quotes).  
Sample Input  
  
2  
3 3 1  
1 2 2  
1 3 4  
2 3 1  
3 1 3  
3 2 1  
1 2 3  
2 3 4  
3 1 8  
  
Sample Output  
  
NO  
YES  
  
Hint  
For farm 1, FJ cannot travel back in time.  

For farm 2, FJ could travel back in time by the cycle 1->2->3->1, arriving
back at his starting location 1 second before he leaves. He could start from
anywhere on the cycle to accomplish this.  

思路以及原理；

在
SPFA算法中，每次松弛的时候，会吧初始点的访问下表变为0，如果图里面存在环的话，SPFA算法是无法结束的，利用这个思维，在一个有n个点的图中，如果不存在自身环下某一个点顶多被所有其他的点相连，这样的话，这个点顶多进队列n-1次，如果存在环，这个点进队的次数一定会大于n-1，利用这个原理，进行一遍SPFA就可以得到答案了

算法 如下

    
    
    #include <iostream>
    #include <queue>
    #include <cmath>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    # define inf 0x3f3f3f3f
    using namespace std;
    int vis[1200];
    int dist[1200];
    int num[1200];
    int n,m,w;
    struct node
    {
        int id;
        int wi;
    } a;
    vector<node>v[1200];
    int SPFA()
    {
        memset(vis,0,sizeof(vis));
        memset(dist,inf,sizeof(dist));
        memset(num,0,sizeof(num));  // 桶排计数的原理
        vis[2]=0;
        dist[2]=0;
        queue<int>q;
        q.push(2);
        num[2]++;
        while(!q.empty())
        {
            int b=q.front();
              if(num[b]>=n)
                    {
                        return 1;
                    }
            q.pop();
            vis[b]=0;
            for(int i=0; i<v[b].size(); i++)
            {
                int id=v[b][i].id;
                int wi=v[b][i].wi;
                if(dist[id]>dist[b]+wi)
                {
                    dist[id]=dist[b]+wi;
                    if(!vis[id])
                    {
                        vis[id]=1;
                        q.push(id);
                        num[id]++;
                    }
                }
            }
        }
        return 0;
    }
    int main ()
    {
        int t;
        int x,y,z;
        scanf("%d",&t);
        while(t--)
        {
            scanf("%d %d %d",&n,&m,&w);
            for(int i=0;i<=n;i++)
            v[i].clear();
            for(int i=0; i<m; i++)
            {
                scanf("%d %d %d",&x,&y,&z);
                a.id=y;
                a.wi=z;
                v[x].push_back(a);
                a.id=x;
                a.wi=z;
                v[y].push_back(a);
            }
            for(int i=0; i<w; i++)
            {
                scanf("%d %d %d",&x,&y, &z);
                a.id=y;
                a.wi=-z;
                v[x].push_back(a);
            }
            int flag=SPFA();
            if(flag) printf("YES\n");
            else  printf("NO\n");
        }
    }
    

  
  

  

