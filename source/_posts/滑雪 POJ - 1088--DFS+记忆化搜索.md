---
title: 滑雪 POJ - 1088--DFS+记忆化搜索
date: 2017-07-29 20:51:03
categories: 数据结构文章标签
---
  
Michael喜欢滑雪百这并不奇怪，
因为滑雪的确很刺激。可是为了获得速度，滑的区域必须向下倾斜，而且当你滑到坡底，你不得不再次走上坡或者等待升降机来载你。Michael想知道载一个区域中最长底滑坡。区域由一个二维数组给出。数组的每个数字代表点的高度。下面是一个例子  
  
1 2 3 4 5  
  
16 17 18 19 6  
  
15 24 25 20 7  
  
14 23<!-- more --> 22 21 8  
  
13 12 11 10 9  
  
  
一个人可以从某个点滑向上下左右相邻四个点之一，当且仅当高度减小。在上面的例子中，一条可滑行的滑坡为24-17-16-1。当然25-24-23-...-3-2-1更长。事实上，这是最长的一条。  
Input  
输入的第一行表示区域的行数R和列数C(1 <= R,C <= 100)。下面是R行，每行有C个整数，代表高度h，0<=h<=10000。  
Output  
输出最长区域的长度。  
Sample Input  
  
5 5  
1 2 3 4 5  
16 17 18 19 6  
15 24 25 20 7  
14 23 22 21 8  
13 12 11 10 9  
  
Sample Output  
  

25

对于每一个点来说，他的最长的长度，从这个点开始四个方向进行比对，假设此点设为map[i][j] , 如果map[i][j]> map[i-1][j] 那么
dp[i][j]=dp[i-1][j]+1 。  

在该点比它四个方向上的点都大的情况下 则满足下列转移方程 dp[i][j] = max(dp[i-1][j], dp[i+1][j] ,
dp[i][j-1], dp[i][j+1] **** )+1

对其进行四个方向上进行深度搜索代码注释见代码

  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <cmath>
    #include <vector>
    #include <queue>
    using namespace std;
    int map[250][250];
    int vis[250][250];
    int dp[250][250];
    int dx[4]= {0,0,-1,1};
    int dy[4]= {1,-1,0,0};
    int n,m,ans;
    int judge(int x, int y)
    {
        if(x<0 || y<0 || x>=n || y>=m) return 0;
        return 1;
    }
    int  dfs(int x, int y)
    {
        if(dp[x][y]>0) return dp[x][y]; //由于dp已经清0了，如果此时的dp不为0，说明这个点的dp已经有值了。
        int k=1;//肯定会存在某一个点，这个点比周围四个点的值都小，此时的dp值为1，即dp的初始值为1，设为k
        for(int i=0;i<4;i++)
        {
            int nx=x+dx[i];
            int ny=y+dy[i];
            if(judge(nx,ny) && map[x][y]>map[nx][ny]) // 满足此条件下，说明此时的dp肯定大于1
            {
                k=max(dfs(nx,ny)+1,k);
            }
        }
        dp[x][y]=k;//对此时的dp[x][y]赋值
        return k;
    }
    int main ()
    {
        while(cin>>n>>m)
        {
            for(int i=0; i<n; i++)
            {
                for(int j=0; j<m; j++)
                    cin>>map[i][j];
            }
            memset(vis,0,sizeof(vis));
            memset(dp,0,sizeof(dp)); // 把此数组全部清0，在dfs里面有用
            int ans=0;
            for(int i=0; i<n; i++)
            {
                for(int j=0; j<m; j++)
                {
    
                    int  t=dfs(i,j);
                    dp[i][j]=t;
                    ans=max(ans,t);
    
                }
            }
            cout<<ans<<endl;
        }
    }
    

  
  

