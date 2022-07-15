---
title: sdut-离散题目5
date: 2017-05-26 23:31:37
categories: 离散数学文章标签
---
离散题目5  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
DaYu收藏了许多电影，他有个志同道合的小伙伴DiGou也收藏了许多电影(电影编号<10000)，这天，DaYu把DiGou的电影拷贝到自己的电脑上，他想知道现在他的电脑上有哪些电影。请你帮他列出他电脑上所有电<!-- more -->影的编号。因为DaYu和DiGou心有灵犀，所以他们的小电影命名方式相同，同样的电影的编号相同。按照编号从小到大输出。  
Input  
  
多组输入,每组的第一行输入两个数m(0 < m < 10000)和n( 0 < n < 10000
)，之后的两行分别有m和n个数字，代表DaYu和DiGou的电影编号。  
Output  
  
对于每组数据，输出一行从小到大排序的电影编号，最后一个数字后面没有空格.  
Example Input  
  
5 5  
1 2 3 4 5  
1 5 3 6 7  
Example Output  
  

1 2 3 4 5 6 7

思路： 数组下标存法，可以简单的过。

    
    
    #include <stdio.h>
    #include <string.h>
    int main ()
    {
        int f[15000];
        int n,m,i,k;
        while(~scanf("%d %d",&n,&m))
        {
            memset(f,0,sizeof(f));
            int max=0;
            for(i=0;i<n;i++)
            {
                scanf("%d",&k);
                if(max<k) max=k;
                f[k]++;
            }
            for(i=0;i<m;i++)
            {
                scanf("%d",&k);
                if(max<k) max=k;
                f[k]++;
            }
            int flag=0;
            for(i=0;i<=max;i++)
            {
                if(f[i]!=0)
                {
                    if(flag==0)
                    {
                    printf("%d",i);
                    flag=1;
                    }
                    else
                        {
                        printf(" %d",i);
                    }
                }
            }
            printf("\n");
        }
    
    }

  
  

