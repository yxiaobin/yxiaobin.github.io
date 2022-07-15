---
title: FatMouse's Speed HDU - 1160 --dp的路径记忆问题
date: 2017-08-09 09:48:24
categories: 数据结构
---
FatMouse believes that the fatter a mouse is, the faster it runs. To disprove
this, you want to take the data on a collection of mice and put as large a
subset of this data as possible into a sequence<!-- more --> so that the weights are
increasing, but the speeds are decreasing.  
Input  
Input contains data for a bunch of mice, one mouse per line, terminated by end
of file.  
  
The data for a particular mouse will consist of a pair of integers: the first
representing its size in grams and the second representing its speed in
centimeters per second. Both integers are between 1 and 10000. The data in
each test case will contain information for at most 1000 mice.  
  
Two mice may have the same weight, the same speed, or even the same weight and
speed.  
Output  
Your program should output a sequence of lines of data; the first line should
contain a number n; the remaining n lines should each contain a single
positive integer (each one representing a mouse). If these n integers are
m[1], m[2],..., m[n] then it must be the case that  
  
W[m[1]] < W[m[2]] < ... < W[m[n]]  
  
and  
  
S[m[1]] > S[m[2]] > ... > S[m[n]]  
  
In order for the answer to be correct, n should be as large as possible.  
All inequalities are strict: weights must be strictly increasing, and speeds
must be strictly decreasing. There may be many correct outputs for a given
input, your program only needs to find one.  
Sample Input  
  
6008 1300  
6000 2100  
500 2000  
1000 4000  
1100 3000  
6000 2000  
8000 1400  
6000 1200  
2000 1900  
  
Sample Output  
  
4  
4  
5  
9  

7

题意：输入到文件结束得到许多对数据，每组的第一个升序排列，第二个降序排列，求最大个数，并把路径记忆

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    struct node
    {
        int id;
        int x;
        int y;
    }a[10020],b;//存储数据
    int dp[10020];//dp用的
    int p[10020];//记录每一个dp最右的时候，继承的上一个的下标
    int pq[10020];//记录位置
    int cmp(node a, node b) // 按第一个升序排列，相同话，讲第二个降序排列
    {
        if(a.x==b.x) return a.y>b.y;
        else
        return a.x<b.x;
    }
    int main ()
    {
        int ax=0;
        while(~scanf("%d %d",&b.x, &b.y))
        {
            if(b.x==0 && b.y==0) break; // 交代码的时候，自动注释掉，这样写容易debug
            b.id=ax+1;
            a[ax]=b;
            ax++;
        }
        sort(a,a+ax,cmp);
        memset(dp,0,sizeof(dp));
        dp[0]=1;
        int Max=dp[0];
        int id=0;
        for(int i=1;i<ax;i++)
        {
           dp[i]=1;
            for(int j=0;j<i;j++)
            {
                if(a[j].x < a[i].x && a[j].y >a[i].y && dp[j]>=dp[i])
                {
                    dp[i]=dp[j]+1;
                    p[i]=j;//记录 得到最优解是继承的上一个 dp[j]
                }
            }
            if(Max<dp[i])
            {
                Max=dp[i];
                id=i; //记录下找到最大值的时候是在id上
            }
        }
        cout<<Max<<endl;
        int k=Max;
        for(int i=k;i>0;i--)//从后往前找的话，就不需要 在把记录数组给逆置一遍了
        {
            pq[i]=a[id].id; //记下最右一个
            id=p[id];//id 一开始指向最大的那个，p[id],指向他的前一个，实现了id的更新链接（类似于bfs记录路径）
        }
        for(int i=1;i<=k;i++)
        cout<<pq[i]<<endl;
    }
    

  
  

  

