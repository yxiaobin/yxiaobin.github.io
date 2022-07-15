---
title: CF—Hot Bath
date: 2017-06-07 17:26:50
categories: 数据结构文章标签
---
  
  
Bob is about to take a hot bath.  
  
There are two taps to fill the bath: a hot water tap and a cold water tap. The
cold water's temperature is t1, and the hot water's temperature is t2. The
co<!-- more -->ld water tap can transmit any integer number of water units per second from
0 to x1, inclusive. Similarly, the hot water tap can transmit from 0 to x2
water units per second.  
  
If y1 water units per second flow through the first tap and y2 water units per
second flow through the second tap, then the resulting bath water temperature
will be:  
  
Bob wants to open both taps so that the bath water temperature was not less
than t0. However, the temperature should be as close as possible to this
value. If there are several optimal variants, Bob chooses the one that lets
fill the bath in the quickest way possible.  
  
Determine how much each tap should be opened so that Bob was pleased with the
result in the end.  
Input  
  
You are given five integers t1, t2, x1, x2 and t0 (1 ≤ t1 ≤ t0 ≤ t2 ≤ 106, 1 ≤
x1, x2 ≤ 106).  
Output  
  
Print two space-separated integers y1 and y2 (0 ≤ y1 ≤ x1, 0 ≤ y2 ≤ x2).  
Example  
Input  
  
10 70 100 100 25  
  
Output  
  
99 33  
  
Input  
  
300 500 1000 1000 300  
  
Output  
  
1000 0  
  
Input  
  
143 456 110 117 273  
  
Output  
  
76 54  
  
Note  
  

In the second sample the hot water tap shouldn't be opened, but the cold water
tap should be opened at full capacity in order to fill the bath in the
quickest way possible.

  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    using namespace std;
    int main ()
    {
        long long int   t1,t2,t0,x1,x2;
        double t,min;
        long long int y1,y2;
        while (cin >>t1>>t2>>x1>>x2>>t0)
        {
           min=1e20;
           while (x1>=0 &&x2>=0)
           {
                t=(double)(t1*x1+t2*x2)/(x1+x2);
                if(t<t0)//小于要求的温度t0，说明此时的冷水的流量过大了，冷水的流量减少
                {
                    x1--;
                }
                else
                {
                    if(t<min)  // 当前流量x1，x2已经满足大于t0了 但是需要寻找满足大于t0的最小值
                               //所以 用一个 比较变量min来记录 当前的最小t
                    {
                        min =t;
                        y1=x1;
                        y2=x2;
                    }
                    x2--;//此时满足t>t0，如果继续减小热水流量，若减少流量后 ，更新后的t依旧大于t0
                         //观察此时的t是否比 min小；如果小于t0了，则继续减少冷水的流量使其继续满足大于
                         //t0在进行，上述操作，一直到x1x2中一个变为0.
                }
           }
            cout<<y1<<" "<<y2<<endl;
        }
        return 0;
    
    }
    

  
  

