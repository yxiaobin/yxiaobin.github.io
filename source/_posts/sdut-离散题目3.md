---
title: sdut-离散题目3
date: 2017-05-26 23:14:40
categories: 离散数学文章标签
---
离散题目3  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
DaYu在新的学习开始学习新的数学知识，一天DaYu学习集合的时候遇到一个问题，他有两个集合A和B，他想知道A是不是B的子集。  
Input  
  
多组输入，每组的第一行有两个数n,m，0 < n,m <<!-- more -->
10^5。表示集合A的大小和集合B的大小。第二行输入n个数表示集合A，第三行输入m个数表示集合B,|data_i| < 10^5  
Output  
  
如果A是B的子集，输出"true"，否则输出"false"。  
Example Input  
  
3 5  
1 2 3  
1 5 4 3 2  
3 5  
1 2 3  
1 4 5 3 6  
Example Output  
  
true  

false

提示 ： 1.输入的数据存在负数情况，所以不能用存下标的方式，如果用的话必须是有加一个偏移量 即 将x存在
a【x+100000】中，但是，本题并没有采用这种方法。

2.判断 A是否为B的子集，首选要保证A的个数小于B（！！！！！！）。

3\. g++ 中的 find 函数，t=find（a,a+n,b)-a 意思是： 对于长度为n的数组a来说，看里面是否有值为b的树，如果有 返回
他在数组的地址，再减去a的首地址就是表示这  个数在数组a的第几个上，如果里面不存在，那么t的值会到a的第n+1个数字上即a【n】。

    
    
    #include <cstdio>
    #include <algorithm>
    using namespace std;
    int a[101000],b[101000];
    void qsort(int a[], int fis , int end)
    {
        int i=fis, j=end,key=a[i];
        if(i>=j) return ;
        while (i<j)
        {
            while (i<j)
            {
                if(a[j] <key)
                {
                    a[i]=a[j];
                    break;
                }
            j--;
            }
            while (i<j)
            {
                if(a[i] >key)
                {
                    a[j]=a[i];
                    break;
                }
                i++;
            }
        }
        a[i]=key;
        qsort(a,fis,i-1);
        qsort(a,i+1,end);
    }
    int main ()
    {
    
        int m,n,i;
        while (~scanf("%d %d",&n,&m))
        {
    
            for(i=0; i<n; i++)
            {
                scanf("%d",&a[i]);
            }
            for(i=0; i<m; i++)
            {
                scanf("%d",&b[i]);
            }
            if(n>m) printf("false\n");
            else {
    
            int flag=1;
            for(i=0;i<n;i++)
            {
                int t = find(b,b+m,a[i])-b;
                if(t==m)
                {
                flag=0;
                break;
                }
            }
            if(flag==0) printf("false\n");
            else printf("true\n");
            }
    
        }
    }
    

  
  

  

