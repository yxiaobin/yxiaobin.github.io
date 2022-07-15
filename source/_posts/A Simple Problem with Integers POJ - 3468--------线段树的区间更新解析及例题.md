---
title: A Simple Problem with Integers POJ - 3468--------线段树的区间更新解析及例题
date: 2017-08-19 21:21:50
categories: 数据结构文章标签
---
传送门： http://poj.org/problem?id=3468  

思路：

典型的线段树区间更新（线段树效率快的精华就是区间更新）

lazy思想：

**
比如现在需要对[a,b]区间值进行加c操作，那么就从根节点[1,n]开始调用update函数进行操作，如果刚好执行到一个子节点，它的节点标记为root：
**

** 如果tree[root].l== a && tree[root<!-- more -->].r == b ,
这时我们可以一步更新此时root节点的segtree[root]的值:  **

** segtree[root] += c* (tree[rt].r - tree[rt].l + 1)，  **

** 注意关键的时刻来了，如果此时按照常规的线段树的update操作，这时候还应该更新root子节点的segtree[]值，  **

**
而Lazy思想恰恰是暂时不更新rt子节点的segtree[]值，到此就return，直到下次需要用到root子节点的值的时候才去更新，这样避免许多可能无用的操作，从而节省时间。
**

**几个错误的地方：**

**1\. 用long long 全部用long long**

**2\. 数组开到4*n**

**3.数据可以时候负数，所以flag数组 不能写if（flag[i] >0） 而要写  **if（flag[i] !=0）**  
**

    
    
    #include <iostream>
    #include<cstring>
    #include<cstdio>
    #include <cmath>
    #include<algorithm>
    using namespace std;
    long long int segtree[100100*4];
    long long int flag[100100*4];
    long long int a[100100];
    
    void pushdown(int root, int l,int r)//向下维护树内数据
    {
        if(flag[root])//如果贪婪标记不是0（说明需要向下进行覆盖区间（或点）的值）
        {
            int mid=(l+r)/2;
            flag[root*2]+=flag[root];//千万记住，这里要写+=，否则会WA。（有可能一下子多次C操作。）
            flag[root*2+1]+=flag[root];
            segtree[root*2]+=(mid-l+1)*flag[root];//千万理解如何覆盖的区间值（对应线段树的图片理解（m-l）+1）是什么意识.
            segtree[root*2+1]+=(r-(mid+1)+1)*flag[root];
            flag[root]=0;
        }
    }
    void pushup(long long int root)
    {
        segtree[root]=segtree[root*2] + segtree[root*2+1];
    }
    
    void build (long long int root,long long int l,long long  int r)
    {
        if(l==r) segtree[root]=a[l];
        else
        {
            long long int mid= (l+r)/2;
            build(root*2, l, mid);
            build (root*2+1, mid+1, r);
            pushup(root);
        }
    }
    long long int query(long long int root,long long int l ,long long int r,  long long int x, long long int y)
    {
        if(x<=l && y>=r) return segtree[root];
        else
        {
            pushdown(root, l,r);
            long long int mid=(l+r)/2;
            if(y<=mid) return query(root*2, l ,mid, x,y);
            else if(x>mid) return query(root*2+1, mid+1, r, x, y);
            else
            return    query(root*2, l , mid, x,y) + query(root*2+1, mid+1, r ,x ,y);
        }
    }
    
    void updata(long long int root, long long int l,long long int r,long long int x, long long int y ,long long int addx)
    {
        if(x<=l && y>=r)
        {
            segtree[root]+=addx*(r-l+1);
            flag[root]+=addx;
        }
        else
        {
            pushdown(root,l,r);
            long long int mid=(l+r)/2;
            if(x<= mid)
            updata(root*2, l, mid, x, y, addx);
            if(y>mid)
            updata(root*2+1, mid+1, r, x, y, addx);
            pushup(root);
        }
    }
    int main ()
    {
        long long  int n,m, x, y, z;
        char c;
        scanf("%lld %lld",&n,&m);
        memset(flag,0,sizeof(flag));
        for(int i=1; i<=n;i++) scanf("%lld",&a[i]);
        build(1,1,n);
        for(int i=0; i<m;i++)
        {
            getchar();
            scanf("%c",&c);
            if(c=='Q')
            {
                scanf("%lld %lld",&x,&y);
                printf("%lld\n",query(1,1,n,x,y));
                //cout<<query(1,1,n,x,y)<<endl;
            }
            else
            {
                scanf("%lld %lld %lld",&x,&y,&z);
                updata(1,1,n,x,y,z);
            }
        }
        return 0;
    }
    

  
  

