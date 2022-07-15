---
title: Buildings HDU - 4296  －－－－贪心
date: 2017-08-07 20:58:30
categories: 数据结构
---
Buildings  
Time Limit: 5000/2000 MS (Java/Others) Memory Limit: 32768/32768 K
(Java/Others)  
Total Submission(s): 4544 Accepted Submission(s): 1664  
  
  
Problem Description  
Have you ever heard <!-- more -->the story of Blue.Mary, the great civil engineer? Unlike
Mr. Wolowitz, Dr. Blue.Mary has accomplished many great projects, one of which
is the Guanghua Building.  
The public opinion is that Guanghua Building is nothing more than one of
hundreds of modern skyscrapers recently built in Shanghai, and sadly, they are
all wrong. Blue.Mary the great civil engineer had try a completely new
evolutionary building method in project of Guanghua Building. That is, to
build all the floors at first, then stack them up forming a complete building.  
Believe it or not, he did it (in secret manner). Now you are face the same
problem Blue.Mary once stuck in: Place floors in a good way.  
Each floor has its own weight wi and strength si. When floors are stacked up,
each floor has PDV(Potential Damage Value) equal to (Σwj)-si, where (Σwj)
stands for sum of weight of all floors above.  
Blue.Mary, the great civil engineer, would like to minimize PDV of the whole
building, denoted as the largest PDV of all floors.  
Now, it’s up to you to calculate this value.  
  
  
Input  
There’re several test cases.  
In each test case, in the first line is a single integer N (1 <= N <= 105)
denoting the number of building’s floors. The following N lines specify the
floors. Each of them contains two integers wi and si (0 <= wi, si <= 100000)
separated by single spaces.  
Please process until EOF (End Of File).  
  
  
Output  
For each test case, your program should output a single integer in a single
line - the minimal PDV of the whole building.  
If no floor would be damaged in a optimal configuration (that is, minimal PDV
is non-positive) you should output 0.  
  
  
Sample Input  
  
3  
10 6  
2 3  
5 4  
2  
2 2  
2 2  
3  
10 3  
2 5  
3 3  
  
  
  
Sample Output  
  
1  
0  

2

  

背锅，背锅！！！，今上午再刷ｄｐ，碰到了一个状压ｄｐ，不会放过了，今下午读这个题意的时候，各种觉得这是一个状压ｄｐ，害死队友，背锅背锅…………

题意：
每一个砖块都有自己的承受重力，还有一个自己的重力，他的计算规则为，这块砖上面所有砖的总重力减去他的承受重力得到的值，将所有砖的此值进行比较，找到最大的来表示这一堆的承受破坏力。设计一个方案，使这个破坏力最小

假设上面的砖为s[i],p[i], 下面的砖为s[j],p[j] 那么的话,就有 s[i]-p[j] <s[j]-p[i]， 假如这就是最优的情况，那么
s[i]-p[j] 最小，移相的 s[i]+p[i]最小，并且放在上面，贪心方案找到了！！！！！

和小的放在上面，大的放在下面：

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    struct node
    {
        int x;
        int y;
        int z;
    }a[100100];
    int cmp (node a, node b)
    {
        return a.z<b.z;
    }
    int main ()
    {
        int n;
        while (cin>>n)
        {
            for(int i=0; i<n;i++)
            {
                scanf("%d %d",&a[i].x,&a[i].y);
                a[i].z=a[i].x+a[i].y;
            }
            sort(a,a+n,cmp);
            long long int sum=0;
            for(int i=0;i<n;i++)
            {
                if(i==n-1)
                {
                    sum-=a[i].y;
                }
                else
                {
                    sum+=a[i].x;
                }
            }
            cout<<sum<<endl;
    
        }
    }
    

  
  

