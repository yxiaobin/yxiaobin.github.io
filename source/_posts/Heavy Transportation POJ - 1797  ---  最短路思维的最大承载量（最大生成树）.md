---
title: Heavy Transportation POJ - 1797  ---  最短路思维的最大承载量（最大生成树）
date: 2017-08-01 21:35:28
categories: 数据结构文章标签
---
  
Background  
Hugo Heavy is happy. After the breakdown of the Cargolifter project he can now
expand business. But he needs a clever man who tells him whether there really
is a way from the place his<!-- more --> customer has build his giant steel crane to the
place where it is needed on which all streets can carry the weight.  
Fortunately he already has a plan of the city with all streets and bridges and
all the allowed weights.Unfortunately he has no idea how to find the the
maximum weight capacity in order to tell his customer how heavy the crane may
become. But you surely know.  
  
Problem  
You are given the plan of the city, described by the streets (with weight
limits) between the crossings, which are numbered from 1 to n. Your task is to
find the maximum weight that can be transported from crossing 1 (Hugo's place)
to crossing n (the customer's place). You may assume that there is at least
one path. All streets can be travelled in both directions.  
Input  
The first line contains the number of scenarios (city plans). For each city
the number n of street crossings (1 <= n <= 1000) and number m of streets are
given on the first line. The following m lines contain triples of integers
specifying start and end crossing of the street and the maximum allowed
weight, which is positive and not larger than 1000000. There will be at most
one street between each pair of crossings.  
Output  
The output for every scenario begins with a line containing "Scenario #i:",
where i is the number of the scenario starting at 1. Then print a single line
containing the maximum allowed weight that Hugo can transport to the customer.
Terminate the output for the scenario with a blank line.  
Sample Input  
  
1  
3 3  
1 2 3  
1 3 4  
2 3 5  
  
Sample Output  
  
Scenario #1:  

4

    
    
    #include <iostream>
    #include<cstdio>
    #include <cstring>
    #include <cmath>
    #include <queue>
    #define inf 0x3f3f3f3f
    using namespace std;
    int map[1200][1200];
    int vis[1200];
    int dist[1200];
    void Dijst(int n)
    {
        memset(vis,0,sizeof(vis));
        for(int i=1; i<=n; i++)
            dist[i]=map[1][i];
        vis[1]=0;
        dist[1]=0;
        for(int i=1; i<=n; i++)
        {
            int Max=-100;
            int Max_id=0;
            for(int j=1; j<=n; j++)
            {
                if(!vis[j] && Max<dist[j]) //每次寻找最大的距离先出列
                {
                    Max=dist[j];
                    Max_id=j;
                }
            }
            vis[Max_id]=1;
            for(int j=1; j<=n; j++)
            {
    
                int Min=min(dist[Max_id],map[Max_id][j]);// 间接路径中的最小值
                 dist[j]=max(Min,dist[j]); // 远志与间接路径的最小值进行比较，取大的
            }
        }
    }
    int main ()
    {
        int t,tt=1;;
        int n,m,a,b,c;
        cin >>t;
        while(t--)
        {
            scanf("%d %d",&n,&m);
            memset(map,0,sizeof(map));
            for(int i=0; i<m; i++)
            {
                scanf("%d %d %d",&a,&b,&c);
                if(map[a][b]<c)
                {
                    map[a][b]=c;
                    map[b][a]=c;
                }
            }
            Dijst(n);
            printf("Scenario #%d:\n",tt++);
            printf("%d\n\n",dist[n]); // PE错误，输出两个回车！！！！
        }
        return 0;
    }
    

  
  

