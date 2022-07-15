---
title: sdut-离散题目13
date: 2017-05-27 00:00:31
categories: 离散数学文章标签
---

    离散题目13
    

Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
DaYu平时只顾着看电影，没有学习离散，学期末快考试的时候才慌了神，因为时间不够，因此他决定只复习一个知识点，但是他发现他一个知识点都不会，因此他跑过来请你帮他解决一个问题。求一个集合是否<!-- more -->是自反的。  
Input  
  
第一行输入组数T(T<10)，每组的第一行输入集合元素个数m(m < 100)和对应关系个数n(n <
100)，集合中元素为1,2,…,m，接下来n行每行输入两个数x，y(0 < x, y < 100)  
Output  
  
如果满足自反关系，则输出true，否则输出false。  
Example Input  
  
2  
5 9  
1 1  
1 2  
2 2  
3 3  
2 3  
4 4  
4 5  
5 5  
5 1  
5 8  
1 1  
1 2  
2 2  
3 3  
2 3  
4 4  
4 5  
5 1  
Example Output  
  

true

false

判断是否 自反 的只需要 a[i][j] a[j][i] 都等于1 就可以了

    
    
    #include <stdio.h>
    
    
    #include <string.h>
    #include <algorithm>
    using namespace std;
    int map[130][130];
    int vis[130];
    int n,m;
    int main ()
    {
        int i,j,k,t;
        scanf("%d",&t);
        while(t--)
        {
            scanf("%d %d",&n,&m);
            memset(map,0,sizeof(map));
            while (m--)
            {
                scanf("%d %d",&j,&k);
                map[j][k]=1;
                map[k][j]=1;
            }
            int flag=0;
            for(i=1;i<=n;i++)
            {
                if(map[i][i]==0)
                {
                    flag=1;
                    break;
                }
            }
            if(flag==1) printf("false\n");
            else   printf("true\n");
    
        }
    
    }
    

  
  

