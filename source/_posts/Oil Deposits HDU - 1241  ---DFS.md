---
title: Oil Deposits HDU - 1241  ---DFS
date: 2017-07-29 21:13:21
categories: 数据结构文章标签
---
The GeoSurvComp geologic survey company is responsible for detecting
underground oil deposits. GeoSurvComp works with one large rectangular region
of land at a time, and creates a grid that divides th<!-- more -->e land into numerous
square plots. It then analyzes each plot separately, using sensing equipment
to determine whether or not the plot contains oil. A plot containing oil is
called a pocket. If two pockets are adjacent, then they are part of the same
oil deposit. Oil deposits can be quite large and may contain numerous pockets.
Your job is to determine how many different oil deposits are contained in a
grid.  
Input  
The input file contains one or more grids. Each grid begins with a line
containing m and n, the number of rows and columns in the grid, separated by a
single space. If m = 0 it signals the end of the input; otherwise 1 <= m <=
100 and 1 <= n <= 100. Following this are m lines of n characters each (not
counting the end-of-line characters). Each character corresponds to one plot,
and is either `*', representing the absence of oil, or `@', representing an
oil pocket.  
Output  
For each grid, output the number of distinct oil deposits. Two different
pockets are part of the same oil deposit if they are adjacent horizontally,
vertically, or diagonally. An oil deposit will not contain more than 100
pockets.  
Sample Input  
  
1 1  
*   
3 5  
*@*@*   
**@**  
*@*@*   
1 8  
@@****@*  
5 5  
****@  
*@@*@   
*@**@   
@@@*@  
@@**@  
0 0  
  
Sample Output  
  
0  
1  
2  

2

提示：

从第一个石油点进行跑dfs，把所有周围的石油的vis数组全部标记为1，然后从下一个标记为0的石油跑第二遍dfs，一直遍历完全整个图，数最后的个数就好了

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <cmath>
    #include <vector>
    #include <queue>
    using namespace std;
    char  map[250][250];
    int   vis[250][250];
    int dx[8]= {0,0,-1,1,1,1,-1,-1};
    int dy[8]= {1,-1,0,0,1,-1,1,-1};
    int n,m,ans;
    int judge(int x, int y)
    {
        if(x<0 || y<0 || x>=n || y>=m) return 0;
        if(vis[x][y]) return 0;
        return 1;
    }
    void dfs(int x, int y)
    {
        vis[x][y]=1;
        for(int i=0;i<8;i++)
        {
            int nx=x+dx[i];
            int ny=y+dy[i];
            if(judge(nx,ny) &&map[nx][ny]=='@')
            {
                dfs(nx,ny);
            }
        }
    }
    int main ()
    {
        while(cin>>n>>m)
        {
            memset(vis,0,sizeof(vis));
            if(n==0 && m==0) break;
            for(int i=0; i<n; i++)
            {
                for(int j=0; j<m; j++)
                    cin>>map[i][j];
            }
            int ans=0;
            for(int i=0;i<n;i++)
            {
                for(int j=0;j<m;j++)
                {
                    if(map[i][j]=='@' &&!vis[i][j])
                    {
                        ans++;
                        dfs(i,j);
                    }
                }
            }
            cout<<ans<<endl;
    
        }
    }
    

  
  

  

