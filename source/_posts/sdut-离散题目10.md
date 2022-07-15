---
title: sdut-离散题目10
date: 2017-05-26 23:47:33
categories: 离散数学文章标签
---
离散题目10  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
给定一个数学函数F和两个集合A,B,写一个程序来确定函数是满射。
如果每个可能的像至少有一个变量映射其上(即像集合B中的每个元素在A中都有一个或一个以上的原像)，或者说值域任何元素都有至少有一个变量与之对应，<!-- more -->那这个映射就叫做满射。  
  
Input  
  
多组输入直到文件结束，对于每组输入，第一行先输入一个n（A集合里的元素个数），m（B集合里的元素个数），k（F数学函数关系的条数）。  
0 < n,m < 10000, 0 < k < n;  
第二行输入有n个元素，分别为a1到an；  
第三行输入有m个元素，分别为b1到bn；  
接下来输入有k行，分别为集合A到B的关系  
Output  
  
（一组答案占一行）  
当满足满射关系时输出Yes。  
不满足关系时输出No。  
Example Input  
  
5 3 5  
1 3 5 7 8  
2 5 6  
1 2  
3 6  
5 5  
7 2  
8 6  
Example Output  
  

Yes

思路 ： 数组下标法完美一遍过

    
    
    #include<stdio.h>
    #include <string.h>
    #include <algorithm>
    using namespace std;
    int a[150000];
        int b[150000];
        int c[150000];
        int d[150000];
        int n,m,k,i,x,y;
    int main ()
    {
        while (~scanf("%d%d%d",&n,&m,&k))
        {
            memset(c,0,sizeof(c));
            memset(d,0,sizeof(d));
            for(i=0;i<n;i++)
            {
                scanf("%d",&a[i]);
            }
            for(i=0;i<m;i++)
            {
                scanf("%d",&b[i]);
            }
            for(i=0;i<k;i++)
            {
                scanf("%d %d",&x,&y);
                c[y]++;
                d[x]++;
            }
            int flag=1;
            for(i=0;i<m;i++)
            {
                if(c[b[i]] ==0)
                {
                    flag=0;
                    break;
                }
            }
            for(i=0;i<n;i++)
            {
                if(d[a[i]]>1)
                {
                    flag=0;
                    break;
                }
            }
            if(flag==1) printf("Yes\n");
            else   printf("No\n");
        }
    }
    
    

  
  

