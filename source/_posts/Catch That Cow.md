---
title: Catch That Cow
date: 2017-06-12 17:21:03
categories: 数据结构文章标签
---
Catch That Cow  
Time Limit: 2000MS Memory Limit: 65536KB  
Problem Description  
Farmer John has been informed of the location of a fugitive cow and wants to
catch her immediately. He starts at a poi<!-- more -->nt N (0 ≤ N ≤ 100,000) on a number
line and the cow is at a point K (0 ≤ K ≤ 100,000) on the same number line.
Farmer John has two modes of transportation: walking and teleporting. *
Walking: FJ can move from any point X to the points X - 1 or X + 1 in a single
minute * Teleporting: FJ can move from any point X to the point 2 × X in a
single minute. If the cow, unaware of its pursuit, does not move at all, how
long does it take for Farmer John to retrieve it?  
Input  
Line 1: Two space-separated integers: N and K  
Output  
Line 1: The least amount of time, in minutes, it takes for Farmer John to
catch the fugitive cow.  
Example Input  
  
5 17  
  
Example Output  
  

4

思路：最短路问题，bfs 就可以了。

坑点 数据量是10w 那么数组要开到20w 。

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <queue>
    #include <algorithm>
    using namespace std;
    struct node
    {
        int x;
        int ans;
    }a,b;
    int n,m;
    int vis[310000];
    void bfs(int x)
    {
        queue<struct node>q;
        vis[x]=1;
        a.x=x;
        a.ans=0;
        q.push(a);
        while(!q.empty())
        {
            b=q.front();
            q.pop();
            int nx=b.x;
            if(nx==m)
            {
                printf("%d\n",b.ans);
                return;
            }
            if(nx-1>=0 && vis[nx-1]==0) //保证 nx-1 >=0 ，因为这是数组的下表
            {
                vis[nx-1]=1;
                a.x=nx-1;
                a.ans=b.ans+1;
                q.push(a);
            }
             if(nx<=m && vis[nx+1]==0)
            {
                vis[nx+1]=1;
                a.x=nx+1;
                a.ans=b.ans+1;
                q.push(a);
            }
            if(nx<=m && vis[nx*2]==0)
            {
                vis[nx*2]=1;
                a.x=nx*2;
                a.ans=b.ans+1;
                q.push(a);
            }
    
    
        }
    }
    int main ()
    {
        cin >>n>>m;
        memset(vis,0,sizeof(vis));
        bfs(n);
        return 0;
     }
    

  
  
  

