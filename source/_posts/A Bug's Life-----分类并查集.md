---
title: A Bug's Life-----分类并查集
date: 2017-08-16 20:56:58
categories: 数据结构
---
Description  
Background  
Professor Hopper is researching the sexual behavior of a rare species of bugs.
He assumes that they feature two different genders and that they only interact
with bugs of th<!-- more -->e opposite gender. In his experiment, individual bugs and their
interactions were easy to identify, because numbers were printed on their
backs.  
Problem  
Given a list of bug interactions, decide whether the experiment supports his
assumption of two genders with no homosexual bugs or if it contains some bug
interactions that falsify it.  
  
Input  
The first line of the input contains the number of scenarios. Each scenario
starts with one line giving the number of bugs (at least one, and up to 2000)
and the number of interactions (up to 1000000) separated by a single space. In
the following lines, each interaction is given in the form of two distinct bug
numbers separated by a single space. Bugs are numbered consecutively starting
from one.  
  
Output  
The output for every scenario is a line containing "Scenario #i:", where i is
the number of the scenario starting at 1, followed by one line saying either
"No suspicious bugs found!" if the experiment is consistent with his
assumption about the bugs' sexual behavior, or "Suspicious bugs found!" if
Professor Hopper's assumption is definitely wrong.  
  
Sample Input  
  
2  
3 3  
1 2  
2 3  
1 3  
4 2  
1 2  
3 4  
  
Sample Output  
  
Scenario #1:  
Suspicious bugs found!  
  
Scenario #2:  
No suspicious bugs found!  
  
Hint  
Huge input,scanf is recommended.  
  

Source

思路：

相对于食物链那道题来说，这道题就简单了许多，某一个点与他的根节点只有两种关系，同性和异性，设 同性为0， 异性为1，先给定两只昆虫x，y
如果两个没有共同的根节点，利用并查集给他们找到共同的根节点，并更新与根节点的关系。如果已经有共同的根节点直接比较关系是否相同就可以了  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int pre[21000];
    int b[21000];
    int flag;
    void Init(int n)
    {
        for(int i=0;i<=n;i++)
        {
            pre[i]=i;
            b[i]=0;
        }
    }
    int get_boss(int x)
    {
        if(x==pre[x]) return x;
        else
        {
            int t=get_boss(pre[x]);
            b[x]=(b[x]+b[pre[x]])%2;
            return pre[x]=t;
        }
    }
    void mergy(int x, int y)
    {
        int t1=get_boss(x);
        int t2=get_boss(y);
        if(t1==t2)
        {
            if(b[x]==b[y]) flag=0;//相同的根节点下，关系相同，说明两者同性不可能是恋爱关系
        }
        else
        {
            pre[t2]=t1;
            b[t2]=(b[x]-b[y]+1)%2;//更新根节点的关系
        }
    
    }
    int main ()
    {
        int t,n,m,tt=1,x,y;
        scanf("%d",&t);
        while(t--)
        {
            scanf("%d %d",&n,&m);
            Init(n);
            flag=1;
            for(int i=0;i<m;i++)
            {
                scanf("%d %d",&x,&y);
                mergy(x,y);
            }
            printf("Scenario #%d:\n",tt++);
            if(flag) printf("No suspicious bugs found!\n\n");
            else printf("Suspicious bugs found!\n\n");
        }
    }
    

  
  

