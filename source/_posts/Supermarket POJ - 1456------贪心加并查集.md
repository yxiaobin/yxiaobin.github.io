---
title: Supermarket POJ - 1456------贪心加并查集
date: 2017-08-16 20:04:08
categories: 数据结构
---
    

A supermarket has a set Prod of products on sale. It earns a profit px for
each product x∈Prod sold by a deadline dx that is measured as an integral
number of time units starting from the moment<!-- more --> the sale begins. Each product
takes precisely one unit of time for being sold. A selling schedule is an
ordered subset of products Sell ≤ Prod such that the selling of each product
x∈Sell, according to the ordering of Sell, completes before the deadline dx or
just when dx expires. The profit of the selling schedule is Profit(Sell)=Σ
x∈Sell  px. An optimal selling schedule is a schedule with a maximum profit.  
For example, consider the products Prod={a,b,c,d} with (pa,da)=(50,2),
(pb,db)=(10,1), (pc,dc)=(20,2), and (pd,dd)=(30,1). The possible selling
schedules are listed in table 1. For instance, the schedule Sell={d,a} shows
that the selling of product d starts at time 0 and ends at time 1, while the
selling of product a starts at time 1 and ends at time 2. Each of these
products is sold by its deadline. Sell is the optimal schedule and its profit
is 80.  
![](https://odzkskevi.qnssl.com/f9d071d9c472cbda044241e92bee7393?v=1502530142)  
Write a program that reads sets of products from an input text file and
computes the profit of an optimal selling schedule for each set of products.  

Input  

A set of products starts with an integer 0 <= n <= 10000, which is the number
of products in the set, and continues with n pairs pi di of integers, 1 <= pi
<= 10000 and 1 <= di <= 10000, that designate the profit and the selling
deadline of the i-th product. White spaces can occur freely in input. Input
data terminate with an end of file and are guaranteed correct.

Output  

For each set of products, the program prints on the standard output the profit
of an optimal selling schedule for the set. Each result is printed from the
beginning of a separate line.

Sample Input  
    
    
    4  50 2  10 1   20 2   30 1
    
    7  20 1   2 1   10 3  100 2   8 2
       5 20  50 10
    

Sample Output  
    
    
    80
    185

Hint  

The sample input contains two product sets. The first set encodes the products
from table 1. The second set is for 7 products. The profit of an optimal
schedule for these products is 185.

  

暴力贪心思路--145ms：

第一想法用贪心来做，按照商品价值的大小进行排序，然后设置标记一个数组，从最大的开始取，如果当前截止时间下没有进行出售活动，那么标记变量变为1，同时sum加和，如果当前截止时间已经被占用了，那么从当前时间往前找到第一个没有占用的时间进行这个操作，如果全部占用，此商品放弃。

代码如下：

    
    
    #include <iostream>
    #include<cstdio>
    #include<cstring>
    #include <algorithm>
    using namespace std;
    struct node
    {
        int x;
        int t;
    }a[10010];
    int vis[10010];//标记变量
    int cmp (node a, node b)
    {
        if(a.x == b.x) return a.t>b.t;
        return a.x >b.x;
    
    }
    int main ()
    {
        int n;
        while(~scanf("%d",&n))
        {
            memset(vis,0,sizeof(vis));
            for(int i=0; i<n; i++)
            {
                scanf("%d %d",&a[i].x, &a[i].t);
            }
            sort(a,a+n,cmp);
            int sum=0;
            for(int i=0; i<n; i++)
            {
                for(int j=a[i].t;j>0;j--)
                {
                    if(!vis[j])//寻找到第一个没有占用的时间点进行出售
                    {
                        vis[j]=1;
                        sum+=a[i].x;
                        break;
                    }
                }
            }
            cout<<sum<<endl;
        }
        return 0;
    }

  
并查集思路： 其实并查集就是上述的优化，上了第二层循环，直接去找当前时间的boos节点，如果是初始值，直接使用，如果不是初始值，那么一定是
deadline_time-1 到1 的一个点，直接传，优化了

代码如下

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int pre[10010];
    struct node
    {
        int x;
        int t;
    } a[10010];
    int get_boss(int x)
    {
        if(pre[x]==-1) return x; // 表明是初始值，可以使用
        else
        {
            pre[x]= get_boss(pre[x]);//更新boos值
            return pre[x];
        }
    }
    int cmp (node a, node b)
    {
        if(a.x==b.x) return a.t<b.t;
        return a.x>b.x;
    }
    int main ()
    {
        int n;
        while(~scanf("%d",&n))
        {
            memset(pre,-1,sizeof(pre));//讲数组初始化为-1
            for(int i=0; i<n; i++)
            {
                scanf("%d %d",&a[i].x, &a[i].t);
            }
            sort(a,a+n,cmp);
            int sum=0;
            for(int i=0; i<n;i++)
            {
                int k=get_boss(a[i].t);
                if(k>0)
                {
                    sum+=a[i].x;
                    pre[k]=k-1;//讲当前点与它前一个点进行压缩路径
                }
            }
            cout<<sum<<endl;
        }
        return 0;
    }
    

  
  

