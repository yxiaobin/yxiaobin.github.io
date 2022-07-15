---
title: How Many Answers Are Wrong--HDU3038--------带权并查集
date: 2017-08-15 09:46:04
categories: 数据结构
---
TT and FF are ... friends. Uh... very very good friends -________-b  
  
FF is a bad boy, he is always wooing TT to play the following game with him.
This is a very humdrum game. To begin with, TT sho<!-- more -->uld write down a sequence of
integers-_-!!(bored).  
![](http://acm.hdu.edu.cn/data/images/exe3038-1.JPG)  
Then, FF can choose a continuous subsequence from it(for example the
subsequence from the third to the fifth integer inclusively). After that, FF
will ask TT what the sum of the subsequence he chose is. The next, TT will
answer FF's question. Then, FF can redo this process. In the end, FF must work
out the entire sequence of integers.  
  
Boring~~Boring~~a very very boring game!!! TT doesn't want to play with FF at
all. To punish FF, she often tells FF the wrong answers on purpose.  
  
The bad boy is not a fool man. FF detects some answers are incompatible. Of
course, these contradictions make it difficult to calculate the sequence.  
  
However, TT is a nice and lovely girl. She doesn't have the heart to be hard
on FF. To save time, she guarantees that the answers are all right if there is
no logical mistakes indeed.  
  
What's more, if FF finds an answer to be wrong, he will ignore it when judging
next answers.  
  
But there will be so many questions that poor FF can't make sure whether the
current answer is right or wrong in a moment. So he decides to write a program
to help him with this matter. The program will receive a series of questions
from FF together with the answers FF has received from TT. The aim of this
program is to find how many answers are wrong. Only by ignoring the wrong
answers can FF work out the entire sequence of integers. Poor FF has no time
to do this job. And now he is asking for your help~(Why asking trouble for
himself~~Bad boy)  

  

Input

Line 1: Two integers, N and M (1 <= N <= 200000, 1 <= M <= 40000). Means TT
wrote N integers and FF asked her M questions.  
  
Line 2..M+1: Line i+1 contains three integer: Ai, Bi and Si. Means TT answered
FF that the sum from Ai to Bi is Si. It's guaranteed that 0 < Ai <= Bi <= N.  
  
You can assume that any sum of subsequence is fit in 32-bit integer.  

  

Output

A single line with a integer denotes how many answers are wrong.

  

Sample Input

    
    
      
    
    
       10 5
    1 10 100
    7 10 28
    1 3 32
    4 6 41
    6 6 1
      

  

Sample Output

    
    
      
    
    
       1
      

  
思路：  
最近在刷并查集，各种不顺，今天又碰到了这个带权并查集，真的是完全想不到如何和并查集联系在一起，去看他们的blog，经过百度题解，以及自己的慢慢尝试，有了一点儿的小小的理解：  
如果把区间[a,b]中的a作为根的话，会发现当区间为[a,a]时，a到根结点的值为0，而实际上a根据输入的可以为任意值，所以把a直接作为跟是不可行的。由于0是空着的，所以我们可以把他利用起来，把区间[a,b]的跟结点用a-1表示，则该区间对应的并查集区间为[a-1,b]，我们在定义一个数组b，用来表示该点到他的前驱的距离，具体合并时如何更新sum数组，看代码（写成递归比较方便），需要注意的是，在输入数据中，b始终是不小于a的  
  
  

    
    
    #include <iostream>
    #include <cstring>
    #include <cmath>
    #include <cstdio>
    #define inf 99999999
    using namespace std;
    int a[202000];
    int b[202000];
    int ans;
    int get_boss(int x)
    {
        if(a[x]==x) return x;
        else
        {
            int t=get_boss(a[x]);
            b[x]+=b[a[x]];
            return a[x]=t;
        }
    }
    void mergy(int x, int y,int z)
    {
        int t1,t2;
        t1=get_boss(x);
        t2=get_boss(y);
        if(t1!=t2)
        {
            a[t2]=t1;
            b[t2]=b[x]+z-b[y];
        }
        else if(b[y]-b[x]!=z)
        ans++;
    }
    int main ()
    {
        int n,m,x,y,z;
        while(cin>>n>>m)
        {
            ans=0;
            for(int i=1; i<=n; i++)
            {
                a[i]=i;
                b[i]=0;
            }
            for(int i=0; i<m; i++)
            {
                scanf("%d %d %d",&x,&y,&z);
                mergy(x-1,y,z);
            }
            cout<<ans<<endl;
        }
    
        return 0;
    }
    

