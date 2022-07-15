---
title: POJ---- Pots ----BFS的路径回溯问题
date: 2017-07-23 09:53:59
categories: 数据结构文章标签
---
    

You are given two pots, having the volume of **A** and **B** liters
respectively. The following operations can be performed:

  1. FILL(i) fill the pot **i** (1 ≤ **i** ≤ 2) from the tap; 
  2. <!-- more -->DROP(i) empty the pot **i** to the drain; 
  3. POUR(i,j) pour from pot **i** to pot **j** ; after this operation either the pot **j** is full (and there may be some water left in the pot **i** ), or the pot **i** is empty (and all its contents have been moved to the pot **j** ). 

Write a program to find the shortest possible sequence of these operations
that will yield exactly **C** liters of water in one of the pots.

Input  

On the first and only line are the numbers **A** , **B** , and **C** . These
are all integers in the range from 1 to 100 and **C** ≤max( **A** , **B** ).

Output  

The first line of the output must contain the length of the sequence of
operations **K** . The following **K** lines must each describe one operation.
If there are several sequences of minimal length, output any one of them. If
the desired result can’t be achieved, the first and only line of the file must
contain the word ‘ **impossible** ’.

ｂｆｓ的回溯昨天想了一下午没有想明白，今天百度博客的时候，突然来了灵感，ｂｆｓ是一个盲目搜索的办法，其中用到了队列，代码冗长，大部分的acmer一般都会用ｃ＋＋的ＳＴＬ来做，我的思路是给你所定义的结构体开一个大点的数组，用这个数组来记录你所使用的ＳＴＬ队列里面所有进队出队的元素的顺序，然后在结构体加两个变量，pos
pre，分别表示 pos表示在数组中的位置，pre表示上一个在数组中的位置，找到目标后，然后逆序存进数组中在正序输出就好了

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <queue>
    #include <algorithm>
    using namespace std;
    int s,n,m,as;
    int vis[110][110];
    int  astep[1500];
    int flag;
    struct node
    {
        int x,y;
        int step;
        int k;//选择的路径是哪一条
        int pre; //上一个在队列里面的位置
        int pos;//在队列里的位置
    } a,b,p[1500];
    int px=0;
    void bfs()
    {
        queue<struct node >q;
        a.x=0;
        a.y=0;
        a.k=0;
        a.pre=0;
        a.step=0;
        a.pos=0;
        vis[a.x][a.y]=1;
        q.push(a);
        p[px++]=a;
        int i=0;
        while(!q.empty())
        {
            b=q.front();
            q.pop();
            if(b.x==m ||b.y == m)
            {
                flag=1;
                as=b.step;
                for(int i=as;i>0;i--)
                {
                    astep[i]=b.k;
                    b=p[b.pre];
                }
                cout<<as<<endl;
                return;
            }
            i=1;
            if(i==1)
            {
                a.k=i;
                a.x=s;
                a.y=b.y;
                a.pre=b.pos;
                a.pos=px;
                a.step=b.step+1;
                if(!vis[a.x][a.y])
                {
                    vis[a.x][a.y]=1;
                    q.push(a);
                    p[px++]=a;
                }
                i++;
            }
            if(i==2)
            {
                a.k=i;
                a.x=b.x;
                a.y=n;
                a.pre=b.pos;
                a.pos=px;
                a.step=b.step+1;
                if(!vis[a.x][a.y])
                {
                    vis[a.x][a.y]=1;
                    q.push(a);
                     p[px++]=a;
                }
                i++;
            }
            if(i==3)
            {
                a.k=i;
                a.x=0;
                a.y=b.y;
                a.pre=b.pos;
                a.pos=px;
                a.step=b.step+1;
                if(!vis[a.x][a.y])
                {
                    vis[a.x][a.y]=1;
                    q.push(a);
                     p[px++]=a;
                }
                i++;
            }
            if(i==4)
            {
                a.k=i;
                a.pre=b.pos;
                a.pos=px;
                a.x=b.x;
                a.y=0;
                a.step=b.step+1;
                if(!vis[a.x][a.y])
                {
                    vis[a.x][a.y]=1;
                    q.push(a);
                     p[px++]=a;
    
                }
                i++;
            }
            if(i==5)
            {
                a.k=i;
                a.pre=b.pos;
                a.pos=px;
                if(b.x > n-b.y)
                {
                    a.x=b.x-n+b.y;
                    if(a.x<0)a.x=0;
                    a.y=n;
                    a.step=b.step+1;
                    i++;
                }
                else
                {
                    a.x=0;
                    a.y=b.y+b.x;
                    a.step=b.step+1;
                    i++;
                }
                if(!vis[a.x][a.y])
                {
                    vis[a.x][a.y]=1;
                    q.push(a);
                     p[px++]=a;
                }
            }
            if(i==6)
            {
                a.k=i;
                a.pre=b.pos;
                a.pos=px;
                if(b.y > s-b.x)
                {
                    a.x=s;
                    a.y=b.y-s+b.x;
                    if(a.y<0) a.y=0;
                    a.step=b.step+1;
                }
                else
                {
                    a.x=b.x+b.y;
                    a.y=0;
                    a.step=b.step+1;
                }
                if(!vis[a.x][a.y])
                {
                    vis[a.x][a.y]=1;
                    q.push(a);
                     p[px++]=a;
                }
            }
        }
    }
    int main ()
    {
       while (cin >>s>>n>>m)
       {
        flag=0;
        px=0;
        memset(vis,0,sizeof(vis));
        memset(astep,0,sizeof(astep));
        bfs();
        if(flag==0) cout<<"impossible"<<endl;
        else
        {
            for(int i=1; i<=as; i++)
            {
                switch (astep[i])
                {
                case 1:
                    cout<<"FILL(1)"<<endl;
                    break;
                case 2:
                    cout<<"FILL(2)"<<endl;
                    break;
                case 3:
                    cout<<"DROP(1)"<<endl;
                    break;
                case 4:
                    cout<<"DROP(2)"<<endl;
                    break;
                case 5:
                    cout<<"POUR(1,2)"<<endl;
                    break;
                case 6:
                    cout<<"POUR(2,1)"<<endl;
                    break;
                }
            }
        }
        }
        return 0;
    }
    

  
  

