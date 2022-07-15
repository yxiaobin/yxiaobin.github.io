---
title: J--company
date: 2017-05-10 07:49:27
categories: 数据结构文章标签
---
company

Time Limit: 1000MS Memory Limit: 65536KB

Submit Statistic

Problem Description  
  
There are n kinds of goods in the company, with each of them has a inventory
of and direct unit benefit . <!-- more -->Now you find due to price changes, for any goods
sold on day i, if its direct benefit is val, the total benefit would be i⋅val.  
Beginning from the first day, you can and must sell only one good per day
until you can't or don't want to do so. If you are allowed to leave some goods
unsold, what's the max total benefit you can get in the end?  
Input  
  
The first line contains an integers n(1≤n≤1000).  
The second line contains n integers val1,val2,..,valn(−100≤.≤100).  
The third line contains n integers cnt1,cnt2,..,cntn(1≤≤100).  
Output  
  
Output an integer in a single line, indicating the max total benefit.  
Example Input  
  
4  
-1 -100 5 6   
1 1 1 2  
Example Output  
  
51  
Hint  
  

sell goods whose price with order as -1, 5, 6, 6, the total benefit would be
-1*1 + 5*2 + 6*3 + 6*4 = 51.

  

  

思路：用数组存起来，将其从小到大排序，若只考虑正数的话 只需要
a*i+b*（i+1）+……若加一个负数的话，则正数部分变成了a*(i+1)+b*（i+2）+…… 与原来相比多了 a+b+…… 同时还多了一个负数s

若 a+b +…… >这个负数s的时候， 那么这个负数就要计算在内————进一步抽象
只需要求一下从当前这个负数到数组最后的和是否满足大于等于0，就好了。找到临界部分就可以了。

提示：

1\. 数据量虽然是1000 但是 下面的个数可以是100 相当于1000*100 数组要开的足够大。

2\. 求和 需要 longlongint

    
    
    #include <stdio.h>
    #include <string.h>
    #include <algorithm>
    using namespace std;
    bool cmp(int m, int n)
    {
        return m<n;
    }
    int main ()
    {
        int a[150000];
        int b[150000];
        int n,i,k,j;
        long long  int sum;
        scanf("%d",&n);
        memset(a,0,sizeof(a));
        memset(b,0,sizeof(b));
        for(i=0; i<n; i++)
        {
            scanf("%d",&a[i]);
        }
        for(i=0; i<n; i++)
        {
            scanf("%d",&b[i]);
        }
        j=n;
        for(i=0; i<n; i++)
        {
            if(b[i]>1)
            {
                for(k=1; k<b[i]; k++)
                {
                    a[j]=a[i];
                    j++;
                }
            }
        }
        n=j;
        sort(a,a+n,cmp);
        if(a[n-1] <=0)
        {
            printf("0\n");
        }
        else
        {
            k=0;
            j=0;
            sum=0;
            for(i=n-1; i>=0; i--)
            {
                    j=j+a[i];
                    if(j<=0)
                    {
                        k=i+1;
                        break;
                    }
            }
            int ans=1;
            for(i=k;i<n;i++)
            {
                sum+=a[i]*ans;
                ans++;
            }
            printf("%lld\n",sum);
        }
        return 0;
    
    }
    
    

  
  

