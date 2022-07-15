---
title: sdut-离散题目7
date: 2017-05-26 23:36:39
categories: 离散数学文章标签
---
  
离散题目7  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
DaYu在新的学习开始学习新的数学知识，一天DaYu学习集合的时候遇到一个问题，他有一个集合A和A的子集B，他想用一个二进制串表示集合B。  
Input  
  
多组输入，每组的第一行有两个数n,m，<!-- more -->（0< m < n < 10^5）.  
第二行输入n个数表示集合A，第三行输入m个数表示集合B,|data_i|< 10^5  
Output  
  
输出一个01字符串表示集合B  
Example Input  
  
10 5  
1 2 3 4 5 6 7 8 9 10  
1 3 5 7 8  
Example Output  
  

1010101100

思路： 集合里面的元素x的绝对值小于10^5 所以可以才有加偏移量的方法，总之还是数组下标法（加偏移量）。

    
    
    #include<stdio.h>
    #include<string.h>
    int main ()
    {
        int n,m,i,k[110000],v;
        int a[220000];
        while (scanf("%d %d",&n,&m)!=EOF)
        {
            memset(a,0,sizeof(a));
            for(i=0;i<n;i++)
            {
            scanf("%d",&k[i]);
            a[k[i]+100000]=0;
            }
            for(i=0;i<m;i++)
            {
                scanf("%d",&v);
                a[v+100000]=1;
            }
            for(i=0;i<n;i++)
            {
                printf("%d",a[k[i]+100000]);
            }
            printf("\n");
        }
    }
    

  
  

