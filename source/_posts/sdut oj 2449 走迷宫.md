---
title: sdut oj 2449 走迷宫
date: 2017-05-20 21:08:09
categories: 数据结构文章标签
---
走迷宫  
Time Limit: 1000MS Memory Limit: 65536KB  
Problem Description  
  
一个由n * m 个格子组成的迷宫，起点是(1, 1)， 终点是(n,
m)，每次可以向上下左右四个方向任意走一步，并且有些格子是不能走动，求从起点到终点经过每个格子至多一次的走法数。  
Input  
第一行一个整数T 表示有T 组测试数据。(T <!-- more --><= 110)  
  
对于每组测试数据:  
  
第一行两个整数n, m，表示迷宫有n * m 个格子。(1 <= n, m <= 6, (n, m) !=(1, 1) ) 接下来n 行，每行m
个数。其中第i 行第j 个数是0 表示第i 行第j 个格子可以走，否则是1 表示这个格子不能走，输入保证起点和终点都是都是可以走的。  
  
任意两组测试数据间用一个空行分开。  
Output  
对于每组测试数据，输出一个整数R，表示有R 种走法。  
  
Example Input  
  
3  
2 2  
0 1  
0 0  
2 2  
0 1  
1 0  
2 3  
0 0 0  
0 0 0  
  
Example Output  
  
1  
0  
4  

一个简单的dfs 搜索，  

    
    
    #include <stdio.h>
    #include <string.h>
    #include <algorithm>
    #define M 100+5
    using namespace std;
    int n,m;
    int ans;
    int map[M][M];
    int  bmap[M][M];
    void dfs(int a, int b)
    {
        if(a<0 || a>=n || b<0 || b>=m) return; //考虑越界的情况，此时直接return
        if(a==n-1 && b==m-1)
        {
            ans++;
                return;  //如果此时不return 他会继续向下进行递归，一直到出现越界的情况才结束，此时，会莫名增大ans的值
        }
        if(bmap[a][b]==0 && map[a][b]==0)
        {
            map[a][b]=1;
            dfs(a-1,b);
            dfs(a,b-1);
            dfs(a+1,b);
            dfs(a,b+1);
            map[a][b]=0;
        }
    }
    int main ()
    {
        int t;
        scanf("%d",&t);
        while (t--)
        {
            scanf("%d %d",&n,&m);
            memset(bmap,0,sizeof(bmap));
            for(int i=0; i<n; i++)
            {
                for(int j=0;j<m;j++)
                {
                    scanf("%d",&map[i][j]);
                }
            }
            ans=0;
            dfs(0,0);
            printf("%d\n",ans);
        }
    }
    

  
  

