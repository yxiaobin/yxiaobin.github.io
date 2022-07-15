---
title: Count the Colors -----超详细的线段树的区间染色题解（线段树原来操作可以这么骚Q&_&Q）
date: 2017-08-23 20:45:23
categories: 数据结构文章标签
---
Painting some colored segments on a line, some previously painted segments may
be covered by some the subsequent ones.  
  
Your task is counting the segments of different colors you can see at last. <!-- more --> 
  
  
Input  
  
  
The first line of each data set contains exactly one integer n, 1 <= n <=
8000, equal to the number of colored segments.  
  
Each of the following n lines consists of exactly 3 nonnegative integers
separated by single spaces:  
  
x1 x2 c  
  
x1 and x2 indicate the left endpoint and right endpoint of the segment, c
indicates the color of the segment.  
  
All the numbers are in the range [0, 8000], and they are all integers.  
  
Input may contain several data set, process to the end of file.  
  
  
Output  
  
  
Each line of the output should contain a color index that can be seen from the
top, following the count of the segments of this color, they should be printed
according to the color index.  
  
If some color can't be seen, you shouldn't print it.  
  
Print a blank line after every dataset.  
  
  
Sample Input  
  
  
5  
0 4 4  
0 3 1  
3 4 2  
0 2 2  
0 2 3  
4  
0 1 1  
3 4 1  
1 3 2  
1 3 1  
6  
0 1 0  
1 2 1  
2 3 1  
1 2 0  
2 3 0  
1 2 1  
  
  
Sample Output  
  
  
1 1  
2 1  
3 1  
  
1 1  
  
0 2  

1 1

思路：

这道题的题意不是那么好理解，在综合了 百度谷歌有道等几个老师的讲解之后，自己理解的题意：
对一个区间【0，n】进行染色，颜色可以覆盖，最终显现最后涂该区域颜料的颜色，
未涂色前，该区间是不可见的，只能看到涂了颜色的部分，问n此操作以后，可以看到几条颜色带，并输出该颜色的数量（有序）。

注意：

这道题是给区间染色，不是对点进行染色。举个栗子，假设 有 0 2 3 操作语句，代表着 0到2 之间的线段染成颜色3 而不是对点0 1 2
进行染色。这就迎来了一个问题，如果我们用线段树来思考这道题（因为这是线段树专题的题……）的话，线段树中的叶子节点放什么？根节点放什么？我一开始的想法是在0和1
的 父亲节点放 0 1 区间的颜色， 1 和 2 的父亲放1 2 区间的颜色， 这样的话 对于1 这个节点来说是两个父亲节点的儿子，这样就不是完全二叉树了
。（尴尬……

上述想法没有行通，区间【0,2】 中有三个点，2条线段，
于是我们就想能不能把颜色像普通的线段树一样存进叶子节点里面，这里有三个点，我们只需要两个，我们可以设计一定的规则 选取当中两个点村颜色 假设 选取1 2
于是 0 2 3 的操作我们就转换成了把节点1 2 涂成颜色3 对于 a b c 操作 就是 把 节点 a+1 到 b 全部涂成颜色c；

之后还是想老问题，父亲节点里面放什么。一般的线段树比如区间找最大值，父亲节点就是放他两个孩子节点的最大值，那么对于这到题的情况，父亲节点放什么？
如果放叶子节点的颜色的话，那么他两个叶子节点的颜色不一样，那么这个父亲节点该放什么颜色？那么放叶子节点颜色的种类数，这样对父亲节点可以解决，那么对于爷爷节点种类数该怎么合并（不可能是简单的父亲节点想加）。放什么东西好像都不合适，不然我们就不放东西了，就放初始值-1！（多谢某大佬对渣渣的指点）这样的话，非叶子节点就都是-1。对于区间更新的题目来说，难免避免不了lazy大法（
大佬说这道题不会做是因为没有掌握到lazy大法的精髓……
）由于其父亲节点存初始值，所以可以利用他的父亲节点存住要改变的颜色，通过延迟操作更新叶子节点，理想状态下，处理到最后情况，所有的非叶子节点全部为-1，
叶子节点为该叶子的颜色，统计的时候，只需要对线段树数组中值
!=-1的点进行统计就好了。但是样例都过不了……经过debug发现，存在某些父亲节点的值为-1,子节点没有改变的情况……于是乎，我们需要在处理一遍线段树，
对起父亲节点为-1的情况，将他的子节点处理为父亲节点的值。

剩下的从代码里体会：

  

    
    
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    #include <cstdio>
    using namespace std;
    int segtree[10010*4];
    int a[10010*4];//二次处理线段树
    int num[10010*4];//统计每一种颜色的颜料出现的次数
    //
    void Init () // 初始化
    {
        for(int i=0; i<10010*4; i++)
        {
            segtree[i] = -1;
            flag[i]=-1;
            a[i] = -1;
            num[i] = 0;
        }
    }
    
    //
    void updata(int root, int l, int r, int x, int y, int z)
    {
        if(x<=l && y>=r)
        {
            segtree[root]=z;//父节点变为颜色z，为以后进行lazy操作
            return ;
        }
        int mid =(l+r)/2;
        if(segtree[root] != -1)
        {
            segtree[root*2]=segtree[root];
            segtree[root*2+1]=segtree[root];
            segtree[root] = -1;
        }
        if(x<=mid) updata(root*2, l, mid, x, y, z);
        if(y>mid)  updata(root*2+1, mid+1, r, x, y, z);
        return ;
    }
    //
    void query(int root, int l, int r)
    {
        if(segtree[root]!=-1)// 父节点存在颜色（或者可以理解为这个区间下，颜色唯一）
        {
            for(int i=l ; i<=r; i++)
            {
                a[i]=segtree[root];
            }
        }
        else
        {
            int mid=(l+r)/2;
            if(l!= r)// l，r相等的话，代表一个点这个操作无意义
            {
                query(root*2, l, mid);
                query(root*2+1, mid+1, r);
            }
    
        }
    }
    //
    int main ()
    {
        int n,x,y,z;
        while (cin>>n)
        {
            Init();
            for(int i=0; i<n; i++)
            {
                scanf("%d %d %d",&x,&y, &z);
                updata(1,1,8010,x+1,y,z);
            }
            query(1,1,8010);//对区间1 8000 进行涂色
            int i=0;
            while(i<8010)
            {
                while(i<8010 && a[i] == -1)//跳过初始值的点
                    i++;
                if(i>8010)
                    break;
                int t=a[i];
                num[t]++;
                while(i<8010 && a[i]==t)//跳过连续的点
                    i++;
            }
            for(int i=0; i<8010; i++)
            {
                if(num[i] != 0)
                {
                    cout<<i<<" "<<num[i]<<endl;
                }
            }
            cout<<endl;
        }
        return 0;
    }
    

  
  

  

  

