---
title: sdut—离散题目1
date: 2017-05-26 23:04:32
categories: 离散数学文章标签
---
离散题目1  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
创建一个函数，以确定一个整数值是否包含在集合中。  
Input  
  
多组输入。  
首先输入集合的元素数n<=100000。  
接下来的一行输入n 个整数0<=ai<=n。  
接下来的一行输入一个整<!-- more -->数 0<=b<=n。  
Output  
  
（一组答案占一行）,如果存在就输出true,如果不存在就输出false.  
Example Input  
  
5  
1 2 3 4 5  
4  
Example Output  
  

true

思路：开头最简单的离散题， ｎ的数据量不是太大，并且， ａ的值是大于０的。

思路是我们可以采用数组的下标存，将一个数组全部初始化为０，如果集合里面有ｊ，那么ａ【ｊ】＝１；

到时候 看 ａ【ｂ】的值就可以判断 是 true 还是 false 。

    
    
    #include <stdio.h>
    int main ()
    {
        int n,i,x;
        int a[110000];
        while (~scanf("%d",&n))
        {
            for(i=0;i<n;i++)
            {
                scanf("%d",&a[i]);
            }
            scanf("%d",&x);
            int flag=0;
            for(i=0;i<n;i++)
            {
                if(a[i]==x)
                {
                    flag=1;
                    printf("true\n");
                    break;
                }
            }
            if(flag==0) printf("false\n");
    
        }
    }

  
  

