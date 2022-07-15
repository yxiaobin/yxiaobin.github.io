---
title: sdut-离散题目8
date: 2017-05-26 23:39:33
categories: 离散数学文章标签
---
离散题目8  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
现有一个全集U，U={ x | x>=1 && x<=N } 。  
对于U的任意子集A，现在定义一种位集（bitset）Abit用来描述U的子集A： 该位集由1,0组成，长度为N，对于集合A中的任意元素x，集<!-- more -->合Abit
在第x位且仅在第x位有对应的1存在，其余位置为0。  
例如： 对于全集U，其对应的描述位集Ubit = { 111...1 } （N个1）； 对于集合A = { 1,2,3,N }，其对应的描述位集Abit =
{ 1110...01 }；  
Input  
  
多组输入，每组输入包括三行，第一行为集合U的指标参数N( 0< N < = 64
)，第二行为集合A的元素，第三行为集合B的元素，元素之间用空格分割，具体参考示例输入。  
Output  
  
每组输入对应两行输出，第一行为A、B的交集的描述位集。第二行为A、B的并集的描述位集。  
Example Input  
  
10  
1 3 5 7 8  
2 5 6  
Example Output  
  
0000100000  

1110111100

思路： 首选还是不确定每一行的个数，所以还是想到切割字符串，但是，我学会了牛逼的c++的输入流！！！，百度 sstream 函数库的
stringstream 的用法吧

剩下的用数组下标存就好了，总体数据不大，时间不会太长。

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <sstream>
    #include <algorithm>
    using namespace std;
    int c[150];
    int d[150];
    char s[150];
    char v[150];
    int main ()
    {
        int i,k;
       while (~scanf("%d",&k))
        {
            getchar();
            getchar();
            memset(c,0,sizeof(c));
            memset(d,0,sizeof(d));
            string str, line;
            int x;
            getline(cin,str);
            getline(cin,line);
            stringstream ss(str);
            while (ss>>x)
            {
                c[x]=1;
            }
            stringstream s1(line);
            while (s1>>x)
            {
                d[x]=1;
            }
    
            for(i=1;i<=k;i++)
            {
                if(c[i]&&d[i]) printf("1");
                else  printf("0");
            }
            printf("\n");
            for(i=1;i<=k;i++)
            {
                if(c[i]||d[i]) printf("1");
                else  printf("0");
            }
            printf("\n");
        }
    
    }
    

  
  

