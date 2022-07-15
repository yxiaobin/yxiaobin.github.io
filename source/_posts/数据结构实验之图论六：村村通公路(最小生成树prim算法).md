---
title: 数据结构实验之图论六：村村通公路(最小生成树prim算法)
date: 2017-07-27 10:03:10
categories: 数据结构文章标签
---
数据结构实验之图论六：村村通公路  
Time Limit: 1000MS Memory Limit: 65536KB  
Problem Description  
当前农村公路建设正如火如荼的展开，某乡镇政府决定实现村村通公路，工程师现有各个村落之间的原始道路统计数据表，表中列出了各村之间可以建设公路的若干条道路的成本，你的任务是根据给出的数据表，求使得每个村都有公路连通所需要的最低成本。  <!-- more -->
Input  
连续多组数据输入，每组数据包括村落数目N(N <= 1000)和可供选择的道路数目M(M <=
3000)，随后M行对应M条道路，每行给出3个正整数，分别是该条道路直接连通的两个村庄的编号和修建该道路的预算成本，村庄从1～N编号。  
Output  
输出使每个村庄都有公路连通所需要的最低成本，如果输入数据不能使所有村庄畅通，则输出-1，表示有些村庄之间没有路连通。  
Example Input  
  
5 8  
1 2 12  
1 3 9  
1 4 11  
1 5 3  
2 3 6  
2 4 9  
3 4 4  
4 5 6  
  
Example Output  
  

19

edge数组的作用记录两点间边的权值，默认的是所有点中 到点v最小的边值几位edge[v]

book数组的作用是记录某点x是否进入了树中，记录了标记为1，没进入的话标记为0；

每当找到一个点，就不断更新edge数组的边值  

  

    
    
    #include<iostream>
    #include <cstdio>
    #include<algorithm>
    #include <cstring>
    #include <cmath>
    #define inf 0x3f3f3f3f
    using namespace std;
    int map[1200][1200];
    int n,m;
    void Init()
    {
        for(int i=0;i<=n+4;i++)
        {
            for(int j=0;j<=n+4;j++)
            {
                map[i][j]=inf;
            }
        }
    };
    void prim()
    {
        int edge[15000];
        int book[15000];
        memset(book,0,sizeof(book));
        for(int i=1;i<=n;i++)
        {
            edge[i]=map[1][i];
        }
        book[1]=1;
        int sum=0;
        for(int i=2;i<=n;i++)
        {
            int min=inf;
            int minid=1;
            for(int j=2;j<=n;j++)
            {
                if(min>edge[j]&& !book[j])
                {
                    min=edge[j];
                    minid=j;
                }
            }
            sum+=min;
            if(min==inf)
            {
                cout<<-1<<endl;
                return;
            }
            book[minid]=1;
            for(int j=2;j<=n;j++)
            {
                if(!book[j] && map[minid][j]<edge[j])
                {
                    edge[j]=map[minid][j];
                }
            }
        }
        cout<<sum<<endl;
        return ;
    
    }
    int main ()
    {
       while(cin>>n>>m)
       {
        Init(); //
        int x,y,z;
        for(int i=0;i<m;i++)
        {
            cin>>x>>y>>z;
            map[x][y]=z;
            map[y][x]=z;
        }
        prim();
        }
    }
    
    
    /***************************************************
    User name: **********
    Result: Accepted
    Take time: 0ms
    Take Memory: 300KB
    Submit time:
    ****************************************************/

  
  
  

