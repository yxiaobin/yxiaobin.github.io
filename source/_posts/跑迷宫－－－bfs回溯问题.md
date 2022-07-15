---
title: 跑迷宫－－－bfs回溯问题
date: 2017-07-24 20:24:21
categories: 数据结构
---
定义一个二维数组：  


int maze[5][5] = {  

0, 1, 0, 0, 0,  

0, 1, 0, 1, 0,  

0, 0, 0, 0, 0,  

0, 1, 1, 1, 0,  

0, 0, 0, 1, 0,  

};  


它表示一个迷宫，其中的1表示墙壁，0表示可以走的路，只能横着走或竖着走，不能斜着走，要求编程序<!-- more -->找出从左上角到右下角的最短路线。  
Input  
一个5 × 5的二维数组，表示一个迷宫。数据保证有唯一解。  
Output  
左上角到右下角的最短路径，格式如样例所示。  
Sample Input  

0 1 0 0 0  
0 1 0 1 0  
0 0 0 0 0  
0 1 1 1 0  
0 0 0 1 0  

Sample Output  

(0, 0)  
(1, 0)  
(2, 0)  
(2, 1)  
(2, 2)  
(2, 3)  
(2, 4)  
(3, 4)  

(4, 4)

BFS+路径回溯的问题，路径回溯，具体看POJ ----Ｐots 那一篇，搞懂那个之后，这个不是事（逃  


​    
    #include <iostream>
    #include <cstring>
    #include <cstdio>
    #include <algorithm>
    #include <queue>
    using namespace std;
    int map[10][10];
    int vis[10][10];
    struct node
    {
        int x;
        int y;
        int pos;
        int pre;
        int step;
    }p[1000],a,b,op[1000];
    int dx[4]={1,-1,0,0};
    int dy[4]={0,0,1,-1};
    int px;
    void bfs()
    {
        queue<struct node>q;
        a.x=0;
        a.y=0;
        a.pos=0;
        a.pre=0;
        a.step=0;
        vis[a.x][a.y]=1;
        q.push(a);
        p[px++]=a;
        while(!q.empty())
        {
            b=q.front();
            q.pop();
            int nx=b.x;
            int ny=b.y;
            if(nx==4 && ny==4)
            {
               int n=b.step;
                for(int i=b.step; i>=0; i--)
                {
                    op[i]=b;
                    b=p[b.pre];
                }
                for(int i=0;i<=n;i++)
                {
                    printf("(%d, %d)\n",op[i].x, op[i].y);
                }
    
            }
            for(int i=0;i<4;i++)
            {
                if(nx+dx[i]>=0 && nx+dx[i]<5 &&ny+dy[i]>=0 && ny+dy[i]<5 && map[nx+dx[i]][ny+dy[i]]==0 && vis[nx+dx[i]][ny+dy[i]]==0)
                {
    
                    a.x=nx+dx[i];
                    a.y=ny+dy[i];
                    a.pos=px;
                    a.pre=b.pos;
                    a.step=b.step+1;
                    vis[a.x][a.y]=1;
                    q.push(a);
                    p[px++]=a;
                }
            }
    
        }
        return;
    }
    int main ()
    {
        memset(map,0,sizeof(map));
        memset(vis,0,sizeof(vis));
        for(int i=0; i<5;i++)
            for (int j=0; j<5 ;j++)
                cin>>map[i][j];
          bfs();
          return 0;
    }



  

  

