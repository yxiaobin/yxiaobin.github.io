---
title: sdut-离散题目6
date: 2017-05-26 23:33:51
categories: 离散数学文章标签
---
离散题目6  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
bLue 最近忙于收集卡片，已知可收集的卡片一共有 n 种，每种卡片都有唯一的编号。 现在给出 bLue 已经收集到的 m
种卡片，你能告诉他剩下的没收集到的卡片都有什么吗？  
Input  
  
多组数据<!-- more -->，到 EOF 结束（数据组数不超过 100）。  
每组数据第一行输入 2 个整数 n (1 <= n <= 100), m (1 <= m <= n)，分别表示卡片总的种类数和 bLue
已经收集到的种类数。  
第二行输入 n 个从小到大给出的用空格分隔的整数，表示所有可收集卡片的编号。  
第三行输入 m 个从小到大给出的用空格分隔的整数，表示 bLue 收集到的 m 种卡片的编号。  
所有的编号都在 1~100 之间。  
Output  
  
对于每组数据，第一行输出一个整数，表示没有收集到的卡片有多少种，如果大于 0，则在下一行再按从小到大输出具体的编号。  
Example Input  
  
5 3  
1 2 3 4 5  
1 3 5  
3 3  
1 2 3  
1 2 3  
Example Output  
  
2  
2 4  
0  
Hint  
  

第一组示例可以看作： U = {1, 2, 3, 4, 5}，A = {1, 3, 5}，答案即为 A 在 U 中的补集 C = {2, 4}。

提示： 万能的 数组下标存法

    
    
    #include <stdio.h>
    #include <string.h>
    int main ()
    {
        int n,m,i,j,k;
        int f[15000], p[15000];
        while (~scanf("%d %d",&n,&m))
        {
            memset(f,0,sizeof(f));
            memset(p,0,sizeof(p));
            int max=0;
            for(i=0;i<n;i++)
            {
                scanf("%d",&k);
                if(k>max) max=k;
                f[k]++;
            }
            for(i=0;i<m;i++)
            {
                scanf("%d",&k);
                p[k]++;
            }
            int sum=0;
            int a[100];
            j=0;
            for(i=0;i<=max;i++)
            {
                if(f[i]!=0 && p[i]==0)
                {
                    sum++;
                    a[j]=i;
                    j++;
                }
            }
            printf("%d\n",sum);
            for(i=0;i<j;i++)
            {
                printf("%d%c",a[i],i==j-1?'\n':' ');
            }
    
        }
    }
    

  
  

