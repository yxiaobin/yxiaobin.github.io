---
title: 魔戒-BFS求最短路
date: 2017-06-05 21:43:10
categories: 数据结构文章标签
---
魔戒  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
蓝色空间号和万有引力号进入了四维水洼，发现了四维物体--魔戒。  
这里我们把飞船和魔戒都抽象为四维空间中的一个点，分别标为 "S" 和 "E"。空间中可能存在障碍物，标为 "#"，其他为可以通过的位置。  
现在他<!-- more -->们想要尽快到达魔戒进行探索，你能帮他们算出最小时间是最少吗？我们认为飞船每秒只能沿某个坐标轴方向移动一个单位，且不能越出四维空间。  
Input  
  
输入数据有多组（数据组数不超过 30），到 EOF 结束。  
每组输入 4 个数 x, y, z, w 代表四维空间的尺寸（1 <= x, y, z, w <= 30）。  
接下来的空间地图输入按照 x, y, z, w 轴的顺序依次给出，你只要按照下面的坐标关系循环读入即可。  
for 0, x-1  
for 0, y-1  
for 0, z-1  
for 0, w-1  
保证 "S" 和 "E" 唯一。  
Output  
  
对于每组数据，输出一行，到达魔戒所需的最短时间。  
如果无法到达，输出 "WTF"（不包括引号）。  
Example Input  
  
2 2 2 2  
..  
.S  
..  
#.  
#.  
.E  
.#  
..  
2 2 2 2  
..  
.S  
#.  
##  
E.  
.#  
#.  
..  
Example Output  
  
1  

3

总结：1.最短路有
两种情况，一种情况是给你一个地图，让你从起始点开始，把周围上下左右的点按着走一遍，满足题意的到队列里面，第一个到终点的就是最短路。第二种情况就是给你一个矩阵，这时候从初始地点开始，遍历初始地点可以到的所有的点，依次入队列。

2\. 不同于以往的这是一个4维空间的，4维的空间我想象不出来，但是类比二维空间，并且题意要求只能沿着坐标轴移动一个单位，因此只有 x-1 x+1 y-1
y+1 z-1 z+1 w-1 w+1 8种情况，分别遍历就好了。

3.地图这一类的题的话，队里里面不要存点，而是存结构体，结构体中有该点的四位坐标，并且记录好步数，如果存点的话，无法找到这个点的四位坐标。

4\.
良巨帮了很大的忙，代码过长，中间出现了一个小问题，良巨细心地找了出来。又帮我改正了一个大问题：找到了目的点的时候，那个点是最后进队的，而我却输出的是队首的步数，（我确实该看医生了…………谢谢良巨，膜一下）。

5.由于
按照顺序进队列，当a进队列的时候，循环里面是逐个判断a周围的点是否满足题意，每当周围的点可以行走的时候，他的步数就是在a的基础上加上1,。！！！1这点很重要！

  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <queue>
    using namespace std;
    char map[40][40][40][40];
    int vis[40][40][40][40];
    int x,y,z,w;
    int flag;
    struct node
    {
        int a;
        int b;
        int c;
        int d;
        int ans;
    }m,n;
    void bfs(int a, int b, int c, int d)
    {
        queue<struct node >q;
        vis[a][b][c][d]=1;
        m.a=a;
        m.b=b;
        m.c=c;
        m.d=d;
        m.ans=0;
        q.push(m);
        while(!q.empty())
        {
            n=q.front();
            a=n.a;
            b=n.b;
            c=n.c;
            d=n.d;
            q.pop();
            if(a-1>=0 &&map[a-1][b][c][d]!='#' && vis[a-1][b][c][d]==0)
            {
                m.a=a-1;
                m.b=b;
                m.c=c;
                m.d=d;
                m.ans=n.ans+1;
                vis[a-1][b][c][d]=1;
                q.push(m);
                if(map[a-1][b][c][d]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
            if(a+1<x &&map[a+1][b][c][d]!='#' && vis[a+1][b][c][d]==0)
            {
                m.a=a+1;
                m.b=b;
                m.c=c;
                m.d=d;
                m.ans=n.ans+1;
                vis[a+1][b][c][d]=1;
                q.push(m);
                if(map[a+1][b][c][d]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
            if(b-1>=0 &&map[a][b-1][c][d]!='#' && vis[a][b-1][c][d]==0)
            {
                m.a=a;
                m.b=b-1;
                m.c=c;
                m.d=d;
                m.ans=n.ans+1;
                vis[a][b-1][c][d]=1;
                q.push(m);
                if(map[a][b-1][c][d]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
            if(b+1<y &&map[a][b+1][c][d]!='#' && vis[a][b+1][c][d]==0)
            {
                m.a=a;
                m.b=b+1;
                m.c=c;
                m.d=d;
                m.ans=n.ans+1;
                vis[a][b+1][c][d]=1;
                q.push(m);
                if(map[a][b+1][c][d]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
            if(c-1>=0 &&map[a][b][c-1][d]!='#' && vis[a][b][c-1][d]==0)
            {
                m.a=a;
                m.b=b;
                m.c=c-1;
                m.d=d;
                m.ans=n.ans+1;
                vis[a][b][c-1][d]=1;
                q.push(m);
                if(map[a][b][c-1][d]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
            if(c+1<z &&map[a][b][c+1][d]!='#' && vis[a][b][c+1][d]==0)
            {
                m.a=a;
                m.b=b;
                m.c=c+1;
                m.d=d;
                m.ans=n.ans+1;
                vis[a][b][c+1][d]=1;
                q.push(m);
                if(map[a][b][c+1][d]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
            if(d-1>=0 &&map[a][b][c][d-1]!='#' && vis[a][b][c][d-1]==0)
            {
                m.a=a;
                m.b=b;
                m.c=c;
                m.d=d-1;
                m.ans=n.ans+1;
                vis[a][b][c][d-1]=1;
                q.push(m);
                if(map[a][b][c][d-1]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
            if(d+1<w &&map[a][b][c][d+1]!='#' && vis[a][b][c][d+1]==0)
            {
                m.a=a;
                m.b=b;
                m.c=c;
                m.d=d+1;
                m.ans=n.ans+1;
                vis[a][b][c][d+1]=1;
                q.push(m);
                if(map[a][b][c][d+1]=='E')
                {
                        printf("%d\n",m.ans);
                        flag=1;
                        return ;
                }
            }
    
        }
    }
    int main ()
    {
        int i,j,k,l;
        int a,b,c,d;
        while(cin >> x>>y>>z>>w)
        {
            memset(vis,0,sizeof(vis));
            for(i=0; i<x; i++)
                for(j=0; j<y; j++)
                    for(k=0; k<z; k++)
                        for(l=0; l<w; l++)
                        {
                            cin>>map[i][j][k][l];
                            if(map[i][j][k][l]=='S')
                            {
                                a=i;
                                b=j;
                                c=k;
                                d=l;
                            }
                        }
              flag=0;
              bfs(a,b,c,d);
              if(flag==0) printf("WTF\n");
        }
        return 0;
    
    }
    
    

  
  

