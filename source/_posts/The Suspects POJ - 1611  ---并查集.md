---
title: The Suspects POJ - 1611  ---并查集
date: 2017-08-14 19:43:01
categories: 数据结构
---
  
Severe acute respiratory syndrome (SARS), an atypical pneumonia of unknown
aetiology, was recognized as a global threat in mid-March 2003. To minimize
transmission to others, the best strategy is t<!-- more -->o separate the suspects from
others.  
In the Not-Spreading-Your-Sickness University (NSYSU), there are many student
groups. Students in the same group intercommunicate with each other
frequently, and a student may join several groups. To prevent the possible
transmissions of SARS, the NSYSU collects the member lists of all student
groups, and makes the following rule in their standard operation procedure
(SOP).  
Once a member in a group is a suspect, all members in the group are suspects.  
However, they find that it is not easy to identify all the suspects when a
student is recognized as a suspect. Your job is to write a program which finds
all the suspects.  
Input  
The input file contains several cases. Each test case begins with two integers
n and m in a line, where n is the number of students, and m is the number of
groups. You may assume that 0 < n <= 30000 and 0 <= m <= 500. Every student is
numbered by a unique integer between 0 and n−1, and initially student 0 is
recognized as a suspect in all the cases. This line is followed by m member
lists of the groups, one line per group. Each line begins with an integer k by
itself representing the number of members in the group. Following the number
of members, there are k integers representing the students in this group. All
the integers in a line are separated by at least one space.  
A case with n = 0 and m = 0 indicates the end of the input, and need not be
processed.  
Output  
For each case, output the number of suspects in one line.  
Sample Input  
  
100 4  
2 1 2  
5 10 13 11 12 14  
2 0 1  
2 99 2  
200 2  
1 5  
5 1 2 3 4 5  
1 0  
0 0  
  
Sample Output  
  
4  
1  

1

利用并查集中的递归把他们的boos，统一就可以了，不过这个不能是靠左原则了，应该是靠0原则，谁是0，谁是boos  

    
    
    #include <iostream>
    #include <cstring>
    #include <cmath>
    #include <cstdio>
    #define inf 99999999
    
    using namespace std;
    
    int a[30200];
    int get_boss(int x)
    {
        if(a[x]==x) return x;
        else
        {
            a[x]=get_boss(a[x]);
            return a[x];
        }
    }
    void mergy(int x, int y)
    {
        int t1,t2;
        t1=get_boss(x);
        t2=get_boss(y);
        if(t1!=t2)
        {
            if(t2!=0)
            a[t2]=t1;
            else
            a[t1]=t2;
        }
    }
    int main ()
    {
        int n,m,x,y,z;
        while(cin>>n>>m, n||m)
        {
            for(int i=0;i<n;i++)
            a[i]=i;
            for(int i=0;i<m;i++)
            {
                scanf("%d",&x);
                scanf("%d",&y);
                for(int i=0;i<x-1;i++)
                {
                    scanf("%d",&z);
                    mergy(y,z);
                }
            }
            int sum=0;
            for(int i=0;i<n;i++)
            {
                int k=get_boss(i);
                if(k==0)
                {
                    sum++;
                }
            }
            cout<<sum<<endl;
        }
        return 0;
    }
    

  
  

