---
title: Coder HDU - 4288----二分快速排序
date: 2017-08-07 20:32:44
categories: 数据结构
---
In mathematics and computer science, an algorithm describes a set of
procedures or instructions that define a procedure. The term has become
increasing popular since the advent of cheap and reliable c<!-- more -->omputers. Many
companies now employ a single coder to write an algorithm that will replace
many other employees. An added benefit to the employer is that the coder will
also become redundant once their work is done. 1  
You are now the signle coder, and have been assigned a new task writing code,
since your boss would like to replace many other employees (and you when you
become redundant once your task is complete).  
Your code should be able to complete a task to replace these employees who do
nothing all day but eating: make the digest sum.  
By saying “digest sum” we study some properties of data. For the sake of
simplicity, our data is a set of integers. Your code should give response to
following operations:  
1\. add x – add the element x to the set;  
2\. del x – remove the element x from the set;  
3\. sum – find the digest sum of the set. The digest sum should be understood
by  
  
where the set S is written as {a 1, a 2, ... , a k} satisfying a 1 < a 2 < a 3
< ... < a k  
Can you complete this task (and be then fired)?  
\------------------------------------------------------------------------------  
1 See http://uncyclopedia.wikia.com/wiki/Algorithm  
Input  
There’re several test cases.  
In each test case, the first line contains one integer N ( 1 <= N <= 10 5 ),
the number of operations to process.  
Then following is n lines, each one containing one of three operations: “add
x” or “del x” or “sum”.  
You may assume that 1 <= x <= 10 9.  
Please see the sample for detailed format.  
For any “add x” it is guaranteed that x is not currently in the set just
before this operation.  
For any “del x” it is guaranteed that x must currently be in the set just
before this operation.  
Please process until EOF (End Of File).  
Output  
For each operation “sum” please print one line containing exactly one integer
denoting the digest sum of the current set. Print 0 if the set is empty.  
Sample Input  
  
9  
add 1  
add 2  
add 3  
add 4  
add 5  
sum  
add 6  
del 3  
sum  
6  
add 1  
add 3  
add 5  
add 7  
add 9  
sum  
  
Sample Output  
  
3  
4  
5  
  
  
  
  
Hint  
  
C++ maybe run faster than G++ in this problem.  

  

思路：今天这场比赛，全程卡这道题目，ｖｅｃｔｏｒ， ｓｅｔ ， 等各种方法都尝试了，都没有解决，但最后突然发现，这道题利用的二分。

或者说，这道题卡时间的地方也不是二分，是插数的时候，对新数插位置的顺序，如果从头开始找的话，会超时，从后面找的话，就不会超时.

    
    
    #include <iostream>
    #include <algorithm>
    #include <cstdio>
    #include <vector>
    #include <cstring>
    using namespace std;
    int a[100100];
    char s[400];
    int erfen(int fis, int end,int k)
    {
        int i=fis;
        int j=end;
        int mid=(i+j)/2;
        if(a[mid]==k) return mid;
        else if(a[mid]>k) return erfen(fis,mid-1,k);
        else  return erfen(mid+1, end, k);
    }
    int main()
    {
        int n,x,j,i,m;
        while (~scanf("%d",&n))
        {
            m=0;
            while(n--)
            {
                scanf("%s",s);
                if(strcmp(s,"add")==0)
                {
                    scanf("%d",&x);
                    for(j=m++;j>=1;j--)
                    {
                        if(a[j-1]>x)// 这才是　卡时间的　地方，暴力的主要到这里的就过了，没注意的就没有过
                        a[j]=a[j-1];
                        else  break;
                    }
                    a[j]=x;
                }
                else if(strcmp(s,"del")==0)
                {
                    scanf("%d",&x);
                    int d=erfen(0,m,x);
                    for(i=d;i<m-1;i++)
                    {
                        a[i]=a[i+1];
                    }
                    m--;
                }
                else
                {
                    long long int sum=0;
                    for( i=2; i<m; i+=5)
                    {
                        sum+=a[i];
                    }
                    printf("%lld\n",sum);
                }
            }
        }
    }
    

  
  

