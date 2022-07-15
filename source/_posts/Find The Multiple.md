---
title: Find The Multiple
date: 2017-06-07 17:38:34
categories: 数据结构文章标签
---
  
Given a positive integer n, write a program to find out a nonzero multiple m
of n whose decimal representation contains only the digits 0 and 1. You may
assume that n is not greater than 200 and th<!-- more -->ere is a corresponding m
containing no more than 100 decimal digits.  
Input  
The input file may contain multiple test cases. Each line contains a value of
n (1 <= n <= 200). A line containing a zero terminates the input.  
Output  
For each value of n in the input print a line containing the corresponding
value of m. The decimal representation of m must not contain more than 100
digits. If there are multiple solutions for a given value of n, any one of
them is acceptable.  
Sample Input  
  
2  
6  
19  
0  
  
Sample Output  
  
10  
100100100100100100  

111111111111111111

题意理解： 给定一个n的值，找到 一个n的倍数m，并且m的十进制只有0和1 （0 1 10 11 100 101 110 111
………………等）任意一个m都可。

  

    
    
    #include <iostream>
    
    using namespace std;
    int flag; //标记一下是否找打了需要的m
    void dfs(long long int x,  int n, int k) // x代表的找的m,n代表给定的n,k代表递归的次数
    {
        if(flag || k==19) return ; //因为x 定义的longlong，顶多到19位，递归x不难看出，一次增加1位，所以最多递归19次
        if(x%n==0)
        {
            flag=1; //找到了满足条件的m，将标记变量变为1
            cout<<x<<endl;
            return;
        }
        dfs(x*10,n,k+1); //深度遍历 0 10 100 110 ……
        dfs(x*10+1,n,k+1);//深度遍历  1 11 101 111 ……
    
    }
    int main()
    {
        int n;
       while(cin >>n,n)
       {
          flag=0;
          dfs(1,n,0);
       }
       return 0;
    }

  
  

