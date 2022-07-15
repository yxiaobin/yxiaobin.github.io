---
title: Fire Game
date: 2017-06-10 21:14:14
categories: 数据结构文章标签
---
  
  
Fat brother and Maze are playing a kind of special (hentai) game on an N*M
board (N rows, M columns). At the beginning, each grid of this board is
consisting of grass or just empty and then they<!-- more --> start to fire all the grass.
Firstly they choose two grids which are consisting of grass and set fire. As
we all know, the fire can spread among the grass. If the grid (x, y) is firing
at time t, the grid which is adjacent to this grid will fire at time t+1 which
refers to the grid (x+1, y), (x-1, y), (x, y+1), (x, y-1). This process ends
when no new grid get fire. If then all the grid which are consisting of grass
is get fired, Fat brother and Maze will stand in the middle of the grid and
playing a MORE special (hentai) game. (Maybe it’s the OOXX game which
decrypted in the last problem, who knows.)  
  
You can assume that the grass in the board would never burn out and the empty
grid would never get fire.  
  
Note that the two grids they choose can be the same.  
Input  
  
The first line of the date is an integer T, which is the number of the text
cases.  
  
Then T cases follow, each case contains two integers N and M indicate the size
of the board. Then goes N line, each line with M character shows the board.
“#” Indicates the grass. You can assume that there is at least one grid which
is consisting of grass in the board.  
  
1 <= T <=100, 1 <= n <=10, 1 <= m <=10  
Output  
  
For each case, output the case number first, if they can play the MORE special
(hentai) game (fire all the grass), output the minimal time they need to wait
after they set fire, otherwise just output -1. See the sample input and output
for more details.  
Sample Input  
  
4  
3 3  
.#.  
###  
.#.  
3 3  
.#.  
#.#  
.#.  
3 3  
...  
#.#  
...  
3 3  
###  
..#  
#.#  
  
Sample Output  
  
Case 1: 1  
Case 2: -1  
Case 3: 0  

Case 4: 2

思路 ： 这是 一个同时对两个点进行 bfs 的题。其实类比与对一个点进行bfs，两个点和一个点其实一样，只不过一开始的时候进队列进两个就可以了。  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <queue>
    using namespace std;
    struct node
    {
        int x,y;
        int time;
    } a[1500],m,n;//构建一个结构体，存点的坐标，和所需要的时间，数组结构体的作用是把所有的#坐标给记录下来
    int x,y;     // x行y列
    char map[50][50];
    int vis[50][50];
    int dx[5]= {0,0,-1,1};
    int dy[5]= {1,-1,0,0};
    int ax;  // 作为数组结构体的下标，同时也标记了整个map里面到底有多少个#
    int bfs(struct node a, struct node b)
    {
        memset(vis,0,sizeof(vis));  //清0数组
        queue<struct node > q;
        vis[a.x][a.y]=1;
        a.time=0;
        q.push(a);
        vis[b.x][b.y]=1;
        b.time=0;
        q.push(b);
        int sum=0;     // 记录 这一遍bfs 一共搜索到了几个#
        int ans=-1;    // 记录搜完时间， 并且 返回用的，赋初值为负数。
        int flag;
        while(!q.empty())
        {
            m=q.front();
            q.pop();
            flag=1;  //标记变量
            sum++;
            for(int i=0; i<4; i++)
            {
                int nx=m.x+dx[i];
                int ny=m.y+dy[i];
                if(map[nx][ny]=='#' && vis[nx][ny]==0)
                {
                    vis[nx][ny]=1;
                    flag=0;  // 若果还能扫到#，标记变量变为0
                    struct node e;
                    e.x=nx;
                    e.y=ny;
                    e.time=m.time+1;;
                    q.push(e);
                }
            }
            if(flag) // 标记变量依旧为1，说明，此时上述扫到的点周围四个方向依旧没有#了
            {
                ans=max(ans, m.time);  // bfs 搜索进行到这个程度的时候所需要的时间，注意这个时候不一定代表这map里面所有的全部扫了一遍
            }
        }
        if(sum<ax) // 如果队列里面全部空了，还有没扫描到的那么sum小于ax
            ans=999999;
        return ans;
    }
    int main ()
    {
        int t,tt;
        cin >>t;
        tt=1;
        while(t--)
        {
            cin >>x>>y;
            ax=0;
            memset(map,0,sizeof(map));
            for(int i=1; i<=x; i++)
                for(int j=1; j<=y; j++)
                {
                    cin >>map[i][j];
                    if(map[i][j]=='#')
                    {
                        a[ax].x=i;
                        a[ax].y=j;
                        ax++;
                    }
                }
            int mm=99999;
            for(int i=0; i<ax; i++)
                for(int j=0; j<ax; j++)
                {
                    mm=min(mm, bfs (a[i],a[j]));  //  暴力遍历所有的情况，找到最优解
                }
            if(mm==99999) mm=-1;
            printf("Case %d: %d\n",tt++,mm);
        }
        return 0;
    }
    

  
  

