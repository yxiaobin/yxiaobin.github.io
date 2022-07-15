---
title: CodeForces 214B
date: 2017-06-20 22:16:37
categories: 数据结构
---
yxc loves math lessons very much, so he doesn't attend them, unlike wwl. But
now yxc wants to get a good mark for math. For that Ms. lxh, his ACM teacher,
gave him a new task. yxc solved the task imme<!-- more -->diately. Can you?  
  
You are given a set of digits, your task is to find the maximum integer that
you can make from these digits. The made number must be divisible by 2, 3, 5
without a residue. It is permitted to use not all digits from the set, it is
forbidden to use leading zeroes.  
  
Each digit is allowed to occur in the number the same number of times it
occurs in the set.  
  
Input  
A single line contains a single integer n (1 ≤ n ≤ 100000) — the number of
digits in the set. The second line contains n digits, the digits are separated
by a single space.  
  
Output  
On a single line print the answer to the problem. If such number does not
exist, then you should print -1.  
  
Example  
Input  
1  
0  
Output  
0  
Input  
11  
3 4 5 4 5 3 5 3 4 4 0  
Output  
5554443330  
Input  
8  
3 2 5 1 5 2 2 3  
Output  
-1   
Note (You Will Win)  

In the first sample there is only one number you can make — 0. In the second
sample the sought number is 5554443330. In the third sample it is impossible
to make the required number.

题意 差不多 是 最多用 n个 数字组成一个最大的数，这个数可以被2 5 3 整除。以为着末尾数字必须为0，并且 各位之和为3的倍数。

题目卡在了 可以删除一个数，也可以删除两个数上。

如果 全部的和 取模3 余1 那么 删除一个取膜余1 的 或者 两个取模余2 的都可以解决问题。

如果 取模3 余2 那么 可以删除一个取模余2 或者 2个取模余1 的。

如果无法满足上述，倘若有0 输出0 没0的话输出-1

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    using namespace std;
    int main ()
    {
        int n,i,j;
        int  a[15];
        memset(a,0,sizeof(a));
        cin >>n;
        int sum=0;
        for(i=0; i<n; i++)
        {
            cin >>j;
            a[j]++;
            sum+=j;
        }
        if(a[0]==0)
        {
            printf("-1\n");
        }
        else
        {
           int f=0;
           if(sum%3==0) f=1;
           else if(sum%3==1)
           {
             for(i=1;i<=9;i=i+3)
             {
                if(a[i]>=1)
                 {
                    a[i]--;
                     f=1;
                    break;
                 }
             }
             if(f==0)
             {
                for(i=2;i<=9;i=i+3)
                {
                    if(a[i]>=1)
                    {
                        a[i]--;
                        if(a[i]>=1)
                        {
                            a[i]--;
                            f=1;
                            break;
                        }
                        else if(a[i+3]>=1)
                        {
                            a[i+3]--;
                             f=1;
                            break;
                        }
                        else if(a[i+6]>=1)
                        {
                            a[i+6]--;
                             f=1;
                            break;
                        }
                        else
                            f=0;
                    }
                }
             }
           }
            else if(sum%3==2)
           {
             for(i=2;i<=9;i=i+3)
             {
                if(a[i]>=1)
                 {
                    a[i]--;
                     f=1;
                    break;
                 }
             }
             if(f==0)
             {
                for(i=1;i<=9;i=i+3)
                {
                    if(a[i]>=1)
                    {
                        a[i]--;
                        if(a[i]>=1)
                        {
                            a[i]--;
                            f=1;
                            break;
                        }
                        else if(a[i+3]>=1)
                        {
                            a[i+3]--;
                             f=1;
                            break;
                        }
                        else if(a[i+6]>=1)
                        {
                            a[i+6]--;
                             f=1;
                            break;
                        }
                        else
                            f=0;
                    }
                }
             }
           }
            if(f)
            {
                int z=1;
                int y=0;
                for(i=9; i>=0; i--)
                {
                    while (a[i]--)
                    {
                        if(i!=0)
                        {
                            printf("%d",i);
                            y=1;
                            z=0;
                        }
                        else
                        {
                            if(y==1)
                                printf("%d",i);
                        }
    
                    }
                }
                if(z)
                    printf("0\n");
            }
    
        }
        return 0;
    
    
    }

  
  

