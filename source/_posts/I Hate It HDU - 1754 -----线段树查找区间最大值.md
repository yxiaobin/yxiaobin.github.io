---
title: I Hate It HDU - 1754 -----线段树查找区间最大值
date: 2017-08-19 09:41:08
categories: 数据结构文章标签
---
很多学校流行一种比较的习惯。老师们很喜欢询问，从某某到某某当中，分数最高的是多少。  
这让很多学生很反感。  
  
不管你喜不喜欢，现在需要你做的是，就是按照老师的要求，写一个程序，模拟老师的询问。当然，老师有时候需要更新某位同学的成绩。  
Input  
本题目包含多组测试，请处理到文件结束。  
在每个测试的第一行，有两个正整数 N 和 M ( 0<N<=200000,0<M<5000 <!-- more -->)，分别代表学生的数目和操作的数目。  
学生ID编号分别从1编到N。  
第二行包含N个整数，代表这N个学生的初始成绩，其中第i个数代表ID为i的学生的成绩。  
接下来有M行。每一行有一个字符 C (只取'Q'或'U') ，和两个正整数A，B。  
当C为'Q'的时候，表示这是一条询问操作，它询问ID从A到B(包括A,B)的学生当中，成绩最高的是多少。  
当C为'U'的时候，表示这是一条更新操作，要求把ID为A的学生的成绩更改为B。  
Output  
对于每一次询问操作，在一行里面输出最高成绩。  
Sample Input  
  
5 6  
1 2 3 4 5  
Q 1 5  
U 3 6  
Q 3 4  
Q 4 5  
U 2 9  
Q 1 5  
  
Sample Output  
  
5  
6  
5  

9

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int segtree[200010*4];
    int a[200010];
    void build(int root, int l, int r)
    {
        if(l==r)    segtree[root]=a[l];
        else
        {
            int mid=(l+r)/2;
            build(root*2, l, mid);
            build (root*2+1, mid+1, r);
            segtree[root]=max (segtree[root*2], segtree[root*2+1]);
        }
    }
    int  query(int root, int l, int r, int q, int w)
    {
        if(q<=l && w>=r ) return segtree[root];
        else
        {
            int mid=(l+r)/2;
            if(w<=mid) return  query(root*2, l, mid, q, w);
            else if(q>mid) return query(root*2+1, mid+1, r, q, w);
            else
            {
                return max (query(root*2, l, mid, q, w), query(root*2+1, mid+1, r, q, w));
            }
        }
    }
    void updata(int root, int l, int r, int pos, int addx)
    {
        if(l==r && l==pos) segtree[root]=addx;
        else
        {
            int mid=(l+r)/2;
            if(pos<=mid) updata(root*2, l, mid, pos, addx);
            else         updata(root*2+1, mid+1, r, pos, addx);
            segtree[root]=max (segtree[root*2], segtree[root*2+1]);
        }
    
    }
    int main ()
    {
        int n,m,x,y;
        while(~scanf("%d %d",&n,&m))
        {
            for(int i=1; i<=n; i++)
            {
                scanf("%d",&a[i]);
            }
            build(1,1,n);
            char s;
            for(int i=0; i<m; i++)
            {
                getchar();
                scanf("%c %d %d",&s,&x,&y);
                if(s=='Q')
                {
                    cout<<query(1,1,n,x,y)<<endl;
                }
                else
                {
                    updata(1,1,n, x,y);
                }
            }
        }
        return 0;
    }
    

  
  

