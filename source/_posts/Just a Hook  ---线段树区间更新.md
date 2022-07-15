---
title: Just a Hook  ---线段树区间更新
date: 2017-08-21 20:54:05
categories: 数据结构
---
In the game of DotA, Pudge’s meat hook is actually the most horrible thing for
most of the heroes. The hook is made up of several consecutive metallic sticks
which are of the same length.  
  
![](htt<!-- more -->ps://odzkskevi.qnssl.com/779a6c86f4db19106cba2c46a7dafe46?v=1503233606)  
  
Now Pudge wants to do some operations on the hook.  
  
Let us number the consecutive metallic sticks of the hook from 1 to N. For
each operation, Pudge can change the consecutive metallic sticks, numbered
from X to Y, into cupreous sticks, silver sticks or golden sticks.  
The total value of the hook is calculated as the sum of values of N metallic
sticks. More precisely, the value for each kind of stick is calculated as
follows:  
  
For each cupreous stick, the value is 1.  
For each silver stick, the value is 2.  
For each golden stick, the value is 3.  
  
Pudge wants to know the total value of the hook after performing the
operations.  
You may consider the original hook is made up of cupreous sticks.  

       

Input      The input consists of several test cases. The first line of the
input is the number of the cases. There are no more than 10 cases.  
For each case, the first line contains an integer N, 1<=N<=100,000, which is
the number of the sticks of Pudge’s meat hook and the second line contains an
integer Q, 0<=Q<=100,000, which is the number of the operations.  
Next Q lines, each line contains three integers X, Y, 1<=X<=Y<=N, Z, 1<=Z<=3,
which defines an operation: change the sticks numbered from X to Y into the
metal kind Z, where Z=1 represents the cupreous kind, Z=2 represents the
silver kind and Z=3 represents the golden kind.  

Output      For each case, print a number in a line representing the total
value of the hook after the operations. Use the format in the example.  

Sample Input  
    
    
    1
    10
    2
    1 5 2
    5 9 3

Sample Output  
    
    
    Case 1: The total value of the hook is 24.

  

裸线段树区间更新  

  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    typedef long long int LL;
    LL segtree[100100*4];
    LL    flag[100100*4];
    LL       a[100100];
    
    void build (LL root, LL l, LL r)
    {
        if(l==r) segtree[root]=a[l];
        else
        {
            LL mid=(l+r)/2;
            build(root*2, l,mid);
            build(root*2+1, mid+1,r);
            segtree[root]=segtree[root*2]+segtree[root*2+1];
        }
    }
    
    LL query (LL root, LL l, LL r, LL x, LL y)
    {
        if(x<=l &&y>=r) return segtree[root];
        else
        {
            LL mid=(l+r)/2;
            if(flag[root])
            {
                flag[root*2]      = flag[root];
                flag[root*2+1]    = flag[root];
                segtree[root*2]   = (mid-l+1)*flag[root];
                segtree[root*2+1] = (r-mid)*flag[root];
                flag[root]=0;
            }
            if(y<=mid) return query(root*2, l,mid,x, y);
            else if(x>mid) return query(root*2+1, mid+1, r, x, y);
            else
                return  query(root*2, l,mid,x, y) + query(root*2+1, mid+1, r, x, y);
        }
    }
    
    void updata(LL root, LL l, LL r, LL x, LL y, LL addx)
    {
        if(x<=l &&y>=r)
        {
            segtree[root]=addx*(r-l+1);
            flag[root]=addx;
        }
        else
        {
            LL mid=(l+r)/2;
            if(flag[root])
            {
                flag[root*2]= flag[root];
                flag[root*2+1]= flag[root];
                segtree[root*2]=(mid-l+1)*flag[root];
                segtree[root*2+1]=(r-mid)*flag[root];
                flag[root]=0;
            }
            if(x<=mid) updata(root*2, l,mid, x,y, addx);
            if(y>mid) updata(root*2+1,mid+1, r, x, y, addx);
            segtree[root]=segtree[root*2+1]+segtree[root*2];
        }
    }
    int main ()
    {
        int t,tt=1;
        long long  int n,m, x, y, z;
        scanf("%d",&t);
        while (t--)
        {
            scanf("%lld",&n);
            memset(flag,0,sizeof(flag));
            for(int i=1; i<=n; i++) a[i]=1;
            build(1,1,n);
            scanf("%lld",&m);
            for(int i=0; i<m; i++)
            {
                scanf("%lld %lld %lld", &x,&y,&z);
                updata(1,1,n,x,y,z);
            }
            printf("Case %d: The total value of the hook is %lld.\n",tt++, segtree[1]);
        }
        return 0;
    }
    
    
    

  

