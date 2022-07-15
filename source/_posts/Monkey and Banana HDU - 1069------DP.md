---
title: Monkey and Banana HDU - 1069------DP
date: 2017-08-07 09:48:37
categories: 数据结构
---
A group of researchers are designing an experiment to test the IQ of a monkey.
They will hang a banana at the roof of a building, and at the mean time,
provide the monkey with some blocks. If the monk<!-- more -->ey is clever enough, it shall
be able to reach the banana by placing one block on the top another to build a
tower and climb up to get its favorite food.  
  
The researchers have n types of blocks, and an unlimited supply of blocks of
each type. Each type-i block was a rectangular solid with linear dimensions
(xi, yi, zi). A block could be reoriented so that any two of its three
dimensions determined the dimensions of the base and the other dimension was
the height.  
  
They want to make sure that the tallest tower possible by stacking blocks can
reach the roof. The problem is that, in building a tower, one block could only
be placed on top of another block as long as the two base dimensions of the
upper block were both strictly smaller than the corresponding base dimensions
of the lower block because there has to be some space for the monkey to step
on. This meant, for example, that blocks oriented to have equal-sized bases
couldn't be stacked.  
  
Your job is to write a program that determines the height of the tallest tower
the monkey can build with a given set of blocks.  
Input  
The input file will contain one or more test cases. The first line of each
test case contains an integer n,  
representing the number of different blocks in the following data set. The
maximum value for n is 30.  
Each of the next n lines contains three integers representing the values xi,
yi and zi.  
Input is terminated by a value of zero (0) for n.  
Output  
For each test case, print one line containing the case number (they are
numbered sequentially starting from 1) and the height of the tallest possible
tower in the format "Case case: maximum height = height".  
Sample Input  
  
1  
10 20 30  
2  
6 8 10  
5 5 5  
7  
1 1 1  
2 2 2  
3 3 3  
4 4 4  
5 5 5  
6 6 6  
7 7 7  
5  
31 41 59  
26 53 58  
97 93 23  
84 62 64  
33 83 27  
0  
  
Sample Output  
  
Case 1: maximum height = 40  
Case 2: maximum height = 21  
Case 3: maximum height = 28  

Case 4: maximum height = 342

题意：给你ｎ种长宽高规格的箱子，每种箱子有无限个，三个维度，任选其中的两个最底面，按照上方的箱子的‘长宽’小于下方箱子‘长宽’的原则垒箱子，求可以垒的最大高度。

每种规格的箱子就有了三种摆法，用结构体存起各种情况，排序后，ｄｐ一遍就可以啦。

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #define inf 0x7fffff
    using namespace std;
    struct node
    {
        int l;
        int w;
        int s;
        int h;
    } a[12000];
    int n,dp[12000];
    int cmp (node a,node b)
    {
        return a.s>b.s;
    }
    int main ()
    {
        int x,y,z,ax;
        int tt=1;
        while(scanf("%d",&n),n)
        {
            ax=0;
            for(int i=0; i<n; i++)
            {
                scanf("%d %d %d",&x,&y,&z);
                a[ax].l=max(x,y);　//储存每种箱子的三种摆法，并切硬性规定ｌ>w（长度　大于宽度，以后　好比较）
                a[ax].w=min(x,y);
                a[ax].s=x*y;
                a[ax++].h=z;
                //
                a[ax].l=max(z,y);
                a[ax].w=min(z,y);
                a[ax].s=z*y;
                a[ax++].h=x;
                //
                a[ax].l=max(x,z);
                a[ax].w=min(x,z);
                a[ax].s=x*z;
                a[ax++].h=y;
            }
            sort(a,a+ax,cmp);
            dp[0]=a[0].h;
            int Max=dp[0];
            for(int i=1; i<ax; i++)
            {
                dp[i]=a[i].h;
                for(int j=0;j<i;j++)
                {
                    if(a[i].s<a[j].s && a[i].l<a[j].l && a[i].w<a[j].w )//简单的ｄｐ过程
                    {
                        dp[i]=max(dp[j]+a[i].h,dp[i]);
                    }
                }
                Max=max(dp[i],Max);
            }
           printf("Case %d: maximum height = %d\n",tt++,Max);
        }
        return 0;
    }
    

  
  

