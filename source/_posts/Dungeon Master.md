---
title: Dungeon Master
date: 2017-06-06 22:59:36
categories: 数据结构文章标签
---
You are trapped in a 3D dungeon and need to find the quickest way out! The
dungeon is composed of unit cubes which may or may not be filled with rock. It
takes one minute to move one unit north, south<!-- more -->, east, west, up or down. You
cannot move diagonally and the maze is surrounded by solid rock on all sides.  
  
Is an escape possible? If yes, how long will it take?  
Input  
The input consists of a number of dungeons. Each dungeon description starts
with a line containing three integers L, R and C (all limited to 30 in size).  
L is the number of levels making up the dungeon.  
R and C are the number of rows and columns making up the plan of each level.  
Then there will follow L blocks of R lines each containing C characters. Each
character describes one cell of the dungeon. A cell full of rock is indicated
by a '#' and empty cells are represented by a '.'. Your starting position is
indicated by 'S' and the exit by the letter 'E'. There's a single blank line
after each level. Input is terminated by three zeroes for L, R and C.  
Output  
Each maze generates one line of output. If it is possible to reach the exit,
print a line of the form  
Escaped in x minute(s).  
  
where x is replaced by the shortest time it takes to escape.  
If it is not possible to escape, print the line  
Trapped!  
Sample Input  
3 4 5  
S....  
.###.  
.##..  
###.#  
  
#####  
#####  
##.##  
##...  
  
#####  
#####  
#.###  
####E  
  
1 3 3  
S##  
#E#  
###  
  
0 0 0  
Sample Output  
Escaped in 11 minute(s).  

Trapped!

思路 ：校赛的时候 做的 魔戒那道题是一个4维空间可以向8个方向移动

这道题是一个三维空间，向6个方向移动，所以这道题由于做了魔戒，就是一模一样的套路了……

唯一不同的是 每一维空间都需要吃一个回车

另外 cin 的话 ，读字符，就不需要吃空格了，用scanf 的话 就需要吃空格，三维，四维吃空格很麻烦，最好还是用 cin

    
    
        #include <iostream>
        #include <cstdio>
        #include <cstring>
        #include <queue>
        using namespace std;
        char map[40][40][40];
        int vis[40][40][40];
        int x,y,z,w;
        int flag;
        struct node
        {
            int a;
            int b;
            int c;
    
            int ans;
        }m,n;
        void bfs(int a, int b, int c)
        {
            queue<struct node >q;
            vis[a][b][c]=1;
            m.a=a;
            m.b=b;
            m.c=c;
    
            m.ans=0;
            q.push(m);
            while(!q.empty())
            {
                n=q.front();
                a=n.a;
                b=n.b;
                c=n.c;
    
                q.pop();
                if(a-1>=0 &&map[a-1][b][c]!='#' && vis[a-1][b][c]==0)
                {
                    m.a=a-1;
                    m.b=b;
                    m.c=c;
    
                    m.ans=n.ans+1;
                    vis[a-1][b][c]=1;
                    q.push(m);
                    if(map[a-1][b][c]=='E')
                    {
                             printf("Escaped in %d minute(s).",m.ans);
                            flag=1;
                            return ;
                    }
                }
                if(a+1<x &&map[a+1][b][c]!='#' && vis[a+1][b][c]==0)
                {
                    m.a=a+1;
                    m.b=b;
                    m.c=c;
    
                    m.ans=n.ans+1;
                    vis[a+1][b][c]=1;
                    q.push(m);
                    if(map[a+1][b][c]=='E')
                    {
                             printf("Escaped in %d minute(s).",m.ans);
                            flag=1;
                            return ;
                    }
                }
                if(b-1>=0 &&map[a][b-1][c]!='#' && vis[a][b-1][c]==0)
                {
                    m.a=a;
                    m.b=b-1;
                    m.c=c;
    
                    m.ans=n.ans+1;
                    vis[a][b-1][c]=1;
                    q.push(m);
                    if(map[a][b-1][c]=='E')
                    {
                             printf("Escaped in %d minute(s).",m.ans);
                            flag=1;
                            return ;
                    }
                }
                if(b+1<y &&map[a][b+1][c]!='#' && vis[a][b+1][c]==0)
                {
                    m.a=a;
                    m.b=b+1;
                    m.c=c;
    
                    m.ans=n.ans+1;
                    vis[a][b+1][c]=1;
                    q.push(m);
                    if(map[a][b+1][c]=='E')
                    {
                             printf("Escaped in %d minute(s).",m.ans);
                            flag=1;
                            return ;
                    }
                }
                if(c-1>=0 &&map[a][b][c-1]!='#' && vis[a][b][c-1]==0)
                {
                    m.a=a;
                    m.b=b;
                    m.c=c-1;
                    m.ans=n.ans+1;
                    vis[a][b][c-1]=1;
                    q.push(m);
                    if(map[a][b][c-1]=='E')
                    {
                              printf("Escaped in %d minute(s).",m.ans);
                            flag=1;
                            return ;
                    }
                }
                if(c+1<z &&map[a][b][c+1]!='#' && vis[a][b][c+1]==0)
                {
                    m.a=a;
                    m.b=b;
                    m.c=c+1;
                    m.ans=n.ans+1;
                    vis[a][b][c+1]=1;
                    q.push(m);
                    if(map[a][b][c+1]=='E')
                    {
                            printf("Escaped in %d minute(s).",m.ans);
                            flag=1;
                            return ;
                    }
                }
    
    
            }
        }
        int main ()
        {
            int i,j,k;
            int a,b,c;
            while(cin >> x>>y>>z)
            {
                if(x==0 &&y==0 &&z==0) break;
                memset(vis,0,sizeof(vis));
                for(i=0; i<x; i++)
                    for(j=0; j<y; j++)
                        for(k=0; k<z; k++)
                            {
                                cin>>map[i][j][k];
                                if(map[i][j][k]=='S')
                                {
                                    a=i;
                                    b=j;
                                    c=k;
    
                                }
                            }
                  flag=0;
                  bfs(a,b,c);
                  if(flag==0) printf("Trapped!");
                  printf("\n");
            }
            return 0;
    
        }

  
  

