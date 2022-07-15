---
title: sdut-离散题目9
date: 2017-05-26 23:44:04
categories: 离散数学文章标签
---
离散题目9  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
给定一个数学函数F和两个集合A,B,写一个程序来确定函数是单射。  
即A中的任意一个元素唯一的对应一个函数值，并且该值为B集合中的某个元素。  
Input  
  
多组输入。  
首先输入集合的元素数n<<!-- more -->=100000。  
接下来的一行输入n 个整数0<=ai<=n。  
接下来的一行输入n个整数 0<=bi<=n。  
接下来的一行输入2n个整数ci，并且当ci的下标为奇数时表示A集合中的元素，当ci的下标为偶数时表示A集合中元素对应的函数值（即B集合的元素)。  
Output  
  
（一组答案占一行）  
当满足单射关系时输出yes  
不满足关系时输出no  
Example Input  
  
4  
1 3 5 7  
2 5 6 8  
1 2 3 2 5 8 7 6  
2  
1 4  
3 5  
1 3 1 5  
Example Output  
  
yes  

no

坑点： 确保 所有的函数对应关系的 数值 都在两个函数里面，同时也需要保证不能有一个x 对应两个y

    
    
    #include <stdio.h>
    #include <string.h>
    #include<algorithm>
    using namespace std;
    int a[150000];
    int b[150000];
    int A[150000];
    int B[150000];
    int main ()
    {
        int n,i,j;
        while (~scanf("%d",&n) )
        {
              memset(A,0,sizeof(A));
            memset(B,0,sizeof(B));
            for(i=0; i<n; i++)
            {
                scanf("%d",&a[i]);
                A[a[i] ]=1;
            }
            for(i=0; i<n; i++)
            {
                scanf("%d",&b[i]);
                B[b[i] ]=1;
            }
            int x;
            int f=1;
            for(i=0; i<2*n; i++)
            {
                scanf("%d",&x);
                if(i%2==0)
                {
                   if(A[x]==1)
                   {
                       A[x]=0;
                   }
                   else
                    f=0;
                }
    
                else
                {
                     if(B[x]!=1)
                          f=0;
                }
            }
           
            if( f==1) printf("yes\n");
            else        printf("no\n");
        }
    }
    

  
  

