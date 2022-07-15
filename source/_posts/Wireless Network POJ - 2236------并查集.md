---
title: Wireless Network POJ - 2236------并查集
date: 2017-08-14 10:58:58
categories: 数据结构
---
  
An earthquake takes place in Southeast Asia. The ACM (Asia Cooperated Medical
team) have set up a wireless network with the lap computers, but an unexpected
aftershock attacked, all computers in th<!-- more -->e network were all broken. The
computers are repaired one by one, and the network gradually began to work
again. Because of the hardware restricts, each computer can only directly
communicate with the computers that are not farther than d meters from it. But
every computer can be regarded as the intermediary of the communication
between two other computers, that is to say computer A and computer B can
communicate if computer A and computer B can communicate directly or there is
a computer C that can communicate with both A and B.  
  
In the process of repairing the network, workers can take two kinds of
operations at every moment, repairing a computer, or testing if two computers
can communicate. Your job is to answer all the testing operations.  
Input  
The first line contains two integers N and d (1 <= N <= 1001, 0 <= d <=
20000). Here N is the number of computers, which are numbered from 1 to N, and
D is the maximum distance two computers can communicate directly. In the next
N lines, each contains two integers xi, yi (0 <= xi, yi <= 10000), which is
the coordinate of N computers. From the (N+1)-th line to the end of input,
there are operations, which are carried out one by one. Each line contains an
operation in one of following two formats:  
1\. "O p" (1 <= p <= N), which means repairing computer p.  
2\. "S p q" (1 <= p, q <= N), which means testing whether computer p and q can
communicate.  
  
The input will not exceed 300000 lines.  
Output  
For each Testing operation, print "SUCCESS" if the two computers can
communicate, or "FAIL" if not.  
Sample Input  
  
4 1  
0 1  
0 2  
0 3  
0 4  
O 1  
O 2  
O 4  
S 1 4  
O 3  
S 1 4  
  
Sample Output  
  
FAIL  

SUCCESS

思路：

这就是一个变形的并查集，无非是加了一个距离条件，只需要判断就好了，没修一台电脑，就讲这个电脑和已经修好的电脑进行并查集运算，找到他的boos，然后在判断最后输入的两个数的boos
是不是一个就可以了  

    
    
    #include <iostream>
    #include <cstring>
    #include <cmath>
    #include <cstdio>
    #define inf 99999999
    using namespace std;
    int a[1300],tp[1300],tpx;
    struct node
    {
        int x;
        int y;
    }b[1300];
    int  judge(node a, node b,int m)
    {
        double s= sqrt(pow(a.x-b.x,2)+pow(a.y-b.y,2));
        if(s<=m) return 1;
        else  return 0;
    }
    int get_boss(int x)
    {
        if(x==a[x]) return x;
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
            a[t2]=t1;
        }
        return ;
    }
    int main ()
    {
        int n,m,x,y;
        scanf("%d %d",&n,&m);
        //init
        for(int i=1;i<=n;i++)
        a[i]=i;
        for(int i=1; i<=n; i++)
        {
            scanf("%d %d",&b[i].x, &b[i].y);
        }
        char s;
        tpx=0;
        while (cin>>s)
        {
            if(s=='O')
            {
                scanf("%d",&x);
                for(int i=0;i<tpx;i++) // 盲搜，会重复，影响效率
                {
                    if(judge(b[tp[i]],b[x],m))
                    {
                        mergy(tp[i],x);
                    }
                }
                tp[tpx]=x;
                tpx++;
            }
            else if(s=='S')
            {
                scanf("%d %d",&x,&y);
                x=get_boss(x);
                y=get_boss(y);
                if(x==y) printf("SUCCESS\n");
                else  printf("FAIL\n");
            }
        }
        return 0;
    }
    

  

  

