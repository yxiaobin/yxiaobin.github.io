---
title: sdut-离散题目18
date: 2017-05-27 00:23:02
categories: 离散数学文章标签
---
离散题目18  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
给出一个集合A和A上的关系R，求关系R的传递闭包。  
例如：  
A={0,1,2} , R={<0,0>,<1,0>,<2,2>,<1,2>,<2,1>}  
t(R) = {<0,0>,<1,0>,<2<!-- more -->,2>,<2,1>,<1,2>,<1,1>,<2,0>};  
Input  
  
多组输入，输入n、m，集合A={0, 1, …, n-1 }；m代表关系的数量，n、m不超过20.  
Output  
  
每组输入输出t(R)，根据t(R)中序偶的第一个数字升序排序，如果第一个数字相同，根据第二个升序排序。  
Example Input  
  
3 5  
0 0  
1 0  
2 2  
1 2  
2 1  
Example Output  
  
0 0  
1 0  
1 1  
1 2  
2 0  
2 1  

2 2

提示： 数据量 不大，三重for 循环 直接暴力

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int b[150][150];
    int main()
    {
        int n,m,j,i,k;
        while(~scanf("%d%d",&n,&m))
        {
            memset(b,0,sizeof(b));
            for(i=0; i<m; i++)
            {
                scanf("%d %d",&j,&k);
                b[j][k]=1;
            }
            for(i=0; i<n; i++)
                for(j=0; j<n; j++)
                {
                    if(b[j][i]==1)
                    {
                        for(k=0; k<n; k++)
                            if(b[i][k]==1)
                            {
                                b[j][k]=1;
                    
                            }
                    }
                }
                for(i=0;i<n;i++)
                {
                    for(j=0;j<n;j++)
                    {
                        if(b[i][j]==1)
                            printf("%d %d\n",i,j);
                    }
                }
        }
        return 0;
    }

  
  

