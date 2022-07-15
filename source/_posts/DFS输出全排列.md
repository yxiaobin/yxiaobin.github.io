---
title: DFS输出全排列
date: 2018-03-11 15:26:48
categories: 数据结构
---
emmmm。。。

之前的遗留问题，今天又翻了出来。。。

记得课本上这道题是 递归的例题。。。。

递归文化博大精深，没看懂………………

现用dfs解一遍此题

题目链接 ：acm.sdut.edu.cn problem题号搜4165

代码如下：

#include <iostream>  
#include<algorithm>  
#include <queue>  
#include <!-- more --><cstring>  
#include <cstdio>  
using namespace std;  
int vist[150000]; //标记变量  
int step[15000];//记录数据  
int a[20];  
int n;  
void dfs(int x) //x 代表深度， n个数据则说明深度遍历到 x+1 层即结束遍历  
{  
if(x>n) //达到目标  
{  
for(int i=1; i<=n; i++)  
if(i==1)  
cout<<step[i];  
else  
cout<<","<<step[i];  
cout<<endl;  
}  
else  
{  
for(int i=1; i<=n; i++)  
{  
if(!vist[a[i]])  
{  
step[x] = a[i];  
vist[a[i]]=1;  
dfs(x+1);  
vist[a[i]]=0;  
}  
}  
}  
}  
int main ()  
{  
int t;  
cin >> t;  
while(t--)  
{  
cin>>n;  
for(int i=1; i<=n; i++)  
{  
cin>>a[i];  
}  
memset(vist,0,sizeof(vist));  
dfs(1);  
}  
}  

