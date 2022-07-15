---
title: sdut-离散题目16
date: 2017-05-27 00:19:15
categories: 离散数学文章标签
---
离散题目16  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
给出集合A,以及集合A上的关系R,求关系R的自反闭包。  
Input  
  
首先输入t,表示有t组数据.  
每组数据第一行输入n,表示A中有n个数据,接下来一行输入n个数,(4 <= n < 100,<!-- more --> 0 < Ai < 100)  
第二行输入m,代表R中有m对关系(0 < m < 100)  
接下来m行每行输入x,y代表< x,y >这对关系.(从小到大给出关系,如果x相同,按y排列)  
Output  
  
输出题目要求的关系集合,每行输出一对关系,输出顺序按照中的x大小非递减排列,假如x相等按照y大小非递减排列.  
每组数据末尾额外输出一行空行。  
Example Input  
  
1  
5  
1 2 3 4 5  
6  
1 1  
1 2  
2 3  
3 3  
4 5  
5 1  
Example Output  
  
1 1  
1 2  
2 2  
2 3  
3 3  
4 4  
4 5  
5 1  

5 5

提示：只需要在已有的对应关系中 ，将原集合中买有出现的（a，a）的情况补上就好了，这道题还是不叫温和的

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int a[15000];
    int b[1200][1200];
    int main ()
    {
        int n,m,i,j,k,t;
        scanf("%d",&t);
        while (t--)
        {
            memset(b,0,sizeof(b));
            scanf("%d",&n);
            for(i=0;i<n;i++)
            {
                scanf("%d",&a[i]);
                b[a[i]][a[i]]=1;
            }
            scanf("%d",&m);
            for(i=0;i<m;i++)
            {
                scanf("%d %d",&j,&k);
                b[j][k]=1;
            }
            for(i=0;i<n;i++)
            {
                for(j=0;j<n;j++)
                {
                    if(b[a[i]][a[j]]==1)
                        printf("%d %d\n",a[i],a[j]);
                }
            }
            printf("\n");
        }
        return 0;
    
    }
    

  
  

