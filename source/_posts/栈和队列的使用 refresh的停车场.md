---
title: 栈和队列的使用 refresh的停车场
date: 2017-05-31 18:27:33
categories: 数据结构文章标签
---
refresh的停车场  
Time Limit: 1000MS Memory Limit: 65536KB  
Problem Description  
refresh最近发了一笔横财，开了一家停车场。由于土地有限，停车场内停车数量有限，但是要求进停车场的车辆过多。当停车场满时，要进入的车辆会进入便道等待，最先进入便道的车辆会优先  
进入停车场，而且停车场的结构要求只出去的车辆必须是停车场中<!-- more -->最后进去的车辆。现告诉你停车场容量N以及命令数M，以及一些命令（Add num
表示车牌号为num的车辆要进入停车场或便道，  
Del 表示停车场中出去了一辆车，Out 表示便道最前面的车辆不再等待，放弃进入停车场）。假设便道内的车辆不超过1000000.  
Input  
输入为多组数据，每组数据首先输入N和M（0＜ ｎ，ｍ ＜200000），接下来输入M条命令。  
Output  
输入结束后，如果出现停车场内无车辆而出现Del或者便道内无车辆而出现Out,则输出Error,否则输出停车场内的车辆，最后进入的最先输出，无车辆不输出。  
Example Input  
  
2 6  
Add 18353364208  
Add 18353365550  
Add 18353365558  
Add 18353365559  
Del  
Out  
  
Example Output  
  
18353365558  

18353364208

思路 ： 根据题意可以知道，在停车场里面是一个栈，在便道上是一个队列，这道题就是栈的队列的一个共同使用。这是我第一次用c++
里面自带的动态栈和队列来进行做题。有一下几点注意

1\. c++ 里面使用 栈 需要添加 #include<stack>头文件，使用队列添加#include <queue>
头文件，并且必须在#include <iostream> 头文件下进行使用。

2\. 操作 ：q.size()，p.size() 可以动态的知道目前 栈和队列里面有几个元素。q.pop（）， p.pop（）：表示
栈删除栈顶元素，队删除队列的第一个元素。

q.top（）表示栈的栈顶元素值的大小，p.front（）表示 队列的第一个元素的值的大小。  

3\. string 是一个类型，他不是字符串，并且需要用 cin cout 输入输出。

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <stack>
    #include <queue>
    #include <string>
    using namespace std;
    int a[15000], b[15000];
    int main ()
    {
        int n,m,i;
        string s,v;
        while(~scanf("%d %d",&n,&m))
        {
            stack<string>p;
            queue<string>q;
            int flag=0;
            for(i=0;i<m;i++)
            {
                cin >>s;
                if(s=="Add")
                {
                    cin >>v;
                    if(i<n)
                    {
                        p.push(v);
                    }
                    else
                    {
                        q.push(v);
                    }
                }
                else if(s=="Del")
                {
                    if(p.empty())
                    {
                        flag=1;
                    }
                    else
                    {
                        p.pop();
                        if(!q.empty())
                        {
                            p.push(q.front());
                            q.pop();
                        }
                    }
                }
                else if(s=="Out")
                {
    
                    if(q.empty())
                    {
                        flag=1;
                    }
                    else
                    {
                        q.pop();
                    }
                }
            }
            if(flag==1) printf("Error\n");
            else
            {
                while(!p.empty())
                {
                    cout << p.top()<<endl;
                    p.pop();
                }
            }
        }
        return 0;
    }

  
  

