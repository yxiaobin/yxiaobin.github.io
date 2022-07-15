---
title: H - A计划 HDU - 2102----普通BFS注意坑点
date: 2017-07-26 10:44:33
categories: 数据结构文章标签
---
可怜的公主在一次次被魔王掳走一次次被骑士们救回来之后，而今，不幸的她再一次面临生命的考验。魔王已经发出消息说将在T时刻吃掉公主，因为他听信谣言说吃公主的肉也能长生不老。年迈的国王正是心急如焚，告招天下勇士来拯救公主。不过公主早已习以为常，她深信智勇的骑士LJ肯定能将她救出。  
现据密探所报，公主被关在一个两层的迷宫里，迷宫的入口是S（0，0，0），公主的位置用P表示，时空传输机用#表示，墙用*表<!-- more -->示，平地用.表示。骑士们一进入时空传输机就会被转到另一层的相对位置，但如果被转到的位置是墙的话，那骑士们就会被撞死。骑士们在一层中只能前后左右移动，每移动一格花1时刻。层间的移动只能通过时空传输机，且不需要任何时间。  
Input  
输入的第一行C表示共有C个测试数据，每个测试数据的前一行有三个整数N，M，T。 N，M迷宫的大小N*M（1 <= N,M
<=10)。T如上所意。接下去的前N*M表示迷宫的第一层的布置情况，后N*M表示迷宫第二层的布置情况。  
Output  
如果骑士们能够在T时刻能找到公主就输出“YES”，否则输出“NO”。  
Sample Input  
  
1  
5 5 14  
S*#*.  
.#...  
.....  
****.  
...#.  
  
..*.P  
#.*..  
***..  
...*.  
*.#..   
  
Sample Output  
  

YES

坑点：

1.骑士通过传送门到另外一层的条件是a层是传送阵的话， b层不能是墙，也不能是传送阵

2.注意题意理解，骑士到了传送阵会自动传送到另一层。  

    
    
    #include<iostream>
    #include <cstdio>
    #include <cstring>
    #include <queue>
    #include <vector>
    #include <algorithm>
    using namespace std;
    char map[40][40][40];
    int vis[40][40][40];
    int dx[4]= {1,-1,0,0};
    int dy[4]= {0,0,1,-1};
    int n,m,t;
    struct node
    {
        int x, y, z;
        int step;
    } a,b;
    int judge(int x, int y)
    {
        if(x<0|| x>=n ||y<0 ||y>=m) return 0;
        else  return 1;
    };
    void bfs()
    {
        queue<struct node>q;
        a.x=0;
        a.y=0;
        a.z=0;
        a.step=0;
        q.push(a);
        vis[0][0][0]=1;
        while(!q.empty())
        {
            b=q.front();
            q.pop();
            int nx=b.x;
            int ny=b.y;
            int nz=b.z;
            if(map[nx][ny][nz]=='P')
            {
                if(b.step<=t)
                {
                    printf("YES\n");
                }
                else printf("NO\n");
                return ;
            }
            else  if(map[nx][ny][nz]=='#')
            {
                if(nz==0 )
                {
    
                    if(map[nx][ny][nz+1]!='*' && !vis[nx][ny][nz+1]&& map[nx][ny][nz-1]!='#')
                    {
                        a.x=nx;
                        a.y=ny;
                        a.z=nz+1;
                        a.step=b.step;
                        vis[a.x][a.y][a.z]=1;
                        q.push(a);
                    }
                }
                if(nz==1)
                {
    
                    if(map[nx][ny][nz-1]!='*' && !vis[nx][ny][nz-1]&& map[nx][ny][nz-1] !='#')
                    {
                        a.x=nx;
                        a.y=ny;
                        a.z=nz-1;
                        a.step=b.step;
                        vis[a.x][a.y][a.z]=1;
                        q.push(a);
                    }
                }
            }
            else if(map[nx][ny][nz] !='*')
            {
                for(int i=0; i<4; i++)
                {
                    if(judge(nx+dx[i],ny+dy[i]) && !vis[nx+dx[i]][ny+dy[i]][nz]&& map[nx+dx[i]][ny+dy[i]][nz]!='*')
                    {
                        a.x=nx+dx[i];
                        a.y=ny+dy[i];
                        a.z=nz;
                        a.step=b.step+1;
                        vis[a.x][a.y][a.z]=1;
                        q.push(a);
                    }
                }
            }
        }
        printf("NO\n");
    };
    int main ()
    {
        int tt;
        cin>>tt;
        while(tt--)
        {
            cin>>n>>m>>t;
            memset(vis,0,sizeof(vis));
            memset(map,0,sizeof(map));
            for(int i=0; i<n; i++)
            {
                for(int j=0; j<m; j++)
                {
                    cin>>map[i][j][0];
                }
            }
            for(int i=0; i<n; i++)
            {
                for(int j=0; j<m; j++)
                {
                    cin>>map[i][j][1];
                }
            }
            bfs();
        }
        return 0;
    }
    

  

