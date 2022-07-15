---
title: 数据结构实验之图论十：判断给定图是否存在合法拓扑序列---bfs判断又向图的无环问题
date: 2017-12-09 15:59:57
categories: 数据结构
---
Problem Description  
  
给定一个有向图，判断该有向图是否存在一个合法的拓扑序列。  
Input  
  
输入包含多组，每组格式如下。  
第一行包含两个整数n，m，分别代表该有向图的顶点数和边数。(n<=10)  
后面m行每行两个整数a b，表示从a到b有一条有向边。  
  
Output  
  
若给定有向图存在合法拓扑序列，则输出YES；否则输出NO。  
<!-- more -->  
Example Input  
  
1 0  
2 2  
1 2  
2 1  
Example Output  
  
YES  
NO  
Hint  

Author

这道题主要靠拓扑排序的定义，拓扑排序指符在有向无环图中从一个无入度的源点开始出发，在去掉源点以及与源点相连接的边之后，在剩余图中的边、点寻找一个源点直到结束，官方说法如下：

循环执行以下两步，直到不存在入度为0的顶点为止。

  * 选择一个入度为0的顶点并输出之； 
  * 从网中删除此顶点及所有出边（以它为起点的有向边）。 

一个图是否存在合法拓扑序列的充要条件： 有向，无环。

    
    
    #include <iostream>
    #include<cstring>
    #define inf 0x3f3f3f
    using namespace std;
    int mp[1100][1100];
    int dist[1100];
    int vis[1100];
    int n,m,flag;
    void bfs()
    {
        int flag =1;
        int q[1200], head, trail;
        head = trail =0;
        vis[1] =1;
        q[trail++] = 1;
        while(head<trail)
        {
            int k = q[head++];
            for(int i=1;i<=n;i++)
            {
                if(mp[k][i] ==1)
                {
                    if(vis[i] ==1)
                    {
                        flag = 0;
                        break;
                    }
                    else
                    {
                        vis[i] = 1;
                        q[trail++] = i;
                    }
                }
            }
        }
        if(flag ) cout<<"YES"<<endl;
        else  cout<<"NO"<<endl;
    }
    int main()
    {
        while( cin>>n>>m)
        {
            memset(mp,0,sizeof(mp));
            memset(vis,0,sizeof(vis));
            int a, b;
            while(m--)
            {
                cin>>a>>b;
                mp[a][b] = 1;
            }
            bfs();
        }
        return 0;
    }

  
  

  

