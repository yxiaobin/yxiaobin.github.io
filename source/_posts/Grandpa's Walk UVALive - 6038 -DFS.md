---
title: Grandpa's Walk UVALive - 6038 -DFS
date: 2017-07-25 19:47:25
categories: 数据结构文章标签
---
题目链接如下  

[
https://icpcarchive.ecs.baylor.edu/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=4049
](https://icpcarchive.ecs.baylor.edu/index.php?option=com_onlinejudge&Itemid=8&p<!-- more -->age=show_problem&problem=4049)

[ 对图进行深度遍历，数条数就好了  
](https://icpcarchive.ecs.baylor.edu/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=4049)

[
](https://icpcarchive.ecs.baylor.edu/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=4049)

    
    
    #include <iostream>
    #include <cstdio>
    #include<cstring>
    #include<algorithm>
    using namespace std;
    int map[120][120];
    int vis[120][120];
    int ans;
    int n,m;
    struct node
    {
        int x;
        int y;
    } h[120000];
    int hx;
    int dx[4]= {0,0,-1,1};
    int dy[4]= {1,-1,0,0};
    void dfs(int x, int y)
    {
        vis[x][y]=1;
        int flag=0;
        for(int i=0; i<4; i++)
        {
            if(x+dx[i]>0 && y+dy[i]>0 && x+dx[i]<=n && y+dy[i]<=m && !vis[x+dx[i]][y+dy[i]] && map[x][y]>map[x+dx[i]][y+dy[i]])
            {
               flag=1;
               dfs(x+dx[i], y+dy[i]);
            }
        }
        if(!flag) ans++;
        vis[x][y]=0;
    }
    int main ()
    {
        int t;
        cin>>t;
        int tt=1;
        while(t--)
        {
            memset(map,0,sizeof(map));
            memset(vis,0,sizeof(vis));
            cin>>n>>m;
            ans=0;
            for(int i=1; i<=n; i++)
            {
                for(int j=1; j<=m; j++)
                {
                    cin>>map[i][j];
                }
            }
            hx=0;
            for(int i=1; i<=n; i++)
            {
                for(int j=1; j<=m; j++)
                {
                    if(map[i][j]>=map[i-1][j] && map[i][j]>=map[i+1][j] && map[i][j]>=map[i][j-1] &&map[i][j]>=map[i][j+1])
                    {
                        h[hx].x=i;
                        h[hx].y=j;
                        hx++;
                    }
                }
            }
            for(int i=0;i<hx;i++)
            {
                dfs(h[i].x, h[i].y);
            }
            printf("Case #%d: %d\n",tt++,ans);
        }
    }
    

  
  

