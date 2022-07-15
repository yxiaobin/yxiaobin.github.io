---
title: sdut-离散题目11
date: 2017-05-26 23:49:29
categories: 离散数学文章标签
---
离散题目11  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
给定一个数学函数写一个程序来确定该函数是否是双射的  
Input  
  
多组输入。 第一行输入三个整数n,m,k,分别表示集合a中的元素个数，集合b中的元素个数，集合a到b的映射个数。 第二行输入n个数<!-- more -->，代表集合a中的元素。
第三行输入m个数，代表集合b中的元素。接下来k行，每行两个数，代表集合a中的元素x和x在集合b中的像y。  
Output  
  
每组数据输出一行，若F为a到b的双射，输出"YES"， 否则输出"NO"。  
Example Input  
  
5 5 5  
1 2 3 7 8  
2 5 6 9 0  
1 9  
3 2  
2 6  
7 0  
8 5  
Example Output  
  
YES  
Hint  
  
保证集合a中元素无重复，集合b中元素无重复，映射关系无重复（如：{,}）  
1<=n,m,k<=1000  
1<=a[i], b[i]<=10000  

x∈a， y∈b

思路： 满足 元素大于0的要求，可以用数组下标存的方法。

    
    
    #include <stdio.h>
    #include <string.h>
    #include <algorithm>
    using namespace std;
    int a[1500];
    int b[1500];
    int c[1500];
    int A[1500];
    int B[1500];
    int C[1500];
    int main ()
    {
        int n,m,i,j,k;
        while (~scanf("%d %d %d",&n,&m,&k))
        {
            memset(A,0,sizeof(A));
            memset(B,0,sizeof(B));
            memset(C,0,sizeof(C));
            for(i=0;i<n;i++)
            {
                scanf("%d",&a[i]);
                A[a[i] ]++;
            }
            for(i=0;i<m;i++)
            {
                scanf("%d",&b[i]);
                B[b[i]]++;
            }
            int x,y;
            for(i=0;i<k;i++)
            {
              scanf("%d %d",&x,&y);
    
                  A[x]++;
                  B[y]++;
    
            }
            int flag=1;
            for(i=0;i<n;i++)
            {
                if(A[a[i]]!=2 || B[b[i]]!=2)
                {
                    flag=0;
                    break;
                }
            }
            if(flag==1) printf("YES\n");
            else printf("NO\n");
    
    
        }
    }

  
  

