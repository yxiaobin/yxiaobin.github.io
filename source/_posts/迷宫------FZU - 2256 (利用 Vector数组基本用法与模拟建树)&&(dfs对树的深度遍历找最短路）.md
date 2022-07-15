---
title: 迷宫------FZU - 2256 (利用 Vector数组基本用法与模拟建树)&&(dfs对树的深度遍历找最短路）
date: 2017-07-25 11:04:45
categories: 数据结构文章标签
---
一天，YellowStar在人生的道路上迷失了方向，迷迷糊糊之中，它误入了一座迷宫中，幸运的是它在路口处发现了一张迷宫的地图。  
  
经过它的观察，它发现这个迷宫一共有n个房间，并且这n个房间呈现一个有根树结构，它现在所在的1号房间为根，其它每个房间都有一个上级房间，连接第i个房间和它的上级房间Pi的道路长度为Wi。  
  
在地图的背面，记载了这个迷宫中，每个房间拥有一个时空传送门，第i个<!-- more -->房间的传送门可以花费Di单位的时间传送到它的任意一个下级房间中（如果x是y的下级房间，并且y是z的下级房间，那么x也是z的下级房间）。  
  
YellowStar的步行速度为1单位时间走1长度，它现在想知道从1号房间出发，到每一个房间的最少时间。  
Input  
  
包含多组测试数据。  
  
第一行输入n表示n个房间。  
  
第二行输出n个数字，第i个数字Di表示i号房间传送器需要花费的时间。  
  
接下来n-1行，第i行包含两个数字Pi和Wi，表示i+1号房间的上级房间为Pi，道路长度为Wi。  
  
1≤n≤100000  
  
1≤Di, Wi≤10^9  
Output  
  
输出n个数，第i个数表示从1号房间出发到i号房间的最少时间。 (注意，输出最后一个数字后面也要加一个空格)  
Sample Input  
  
5  
99 97 50 123 550  
1 999  
1 10  
3 100  
3 44  
  
Sample Output  
  
0 99 10 60 54  
  
Hint  
  
初始在1号房间，到1号房间的代价为0。  
  
通过1号房间的传送门传送到2号房间，到2号房间的代价为99。  
  
通过1号房间走到3号房间，到3号房间的代价为10。  
  
通过1号房间走到3号房间，在通过3号房间的传送门传送到4号房间，到4号房间的代价为60。  
  

通过1号房间走到3号房间，在通过3号房间走到5号房间，到5号房间的代价为54。

  

思路：

一：vector数组的建树过程

1\. vector基本操作：  
  
(1). 容量  
  
向量大小： vec.size();  
向量最大容量： vec.max_size();  
更改向量大小： vec.resize();  
向量真实大小： vec.capacity();  
向量判空： vec.empty();  
减少向量大小到满足元素所占存储空间的大小： vec.shrink_to_fit(); //shrink_to_fit  
  
(2). 修改  
  
多个元素赋值： vec.assign(); //类似于初始化时用数组进行赋值  
末尾添加元素： vec.push_back();  
末尾删除元素： vec.pop_back();  
任意位置插入元素： vec.insert();  
任意位置删除元素： vec.erase();  
交换两个向量的元素： vec.swap();  
清空向量元素： vec.clear();  
  
(3)迭代器  
  
开始指针：vec.begin();  
末尾指针：vec.end(); //指向最后一个元素的下一个位置  
指向常量的开始指针： vec.cbegin(); //意思就是不能通过这个指针来修改所指的内容，但还是可以通过其他方式修改的，而且指针也是可以移动的。  
指向常量的末尾指针： vec.cend();  
  
(4)元素的访问  
  
下标访问： vec[1]; //并不会检查是否越界  
at方法访问： vec.at(1); //以上两者的区别就是at会检查是否越界，是则抛出out of range异常  
访问第一个元素： vec.front();  
访问最后一个元素： vec.back();  
返回一个指针： int* p = vec.data();
//可行的原因在于vector在内存中就是一个连续存储的数组，所以可以返回一个指针指向这个数组。这是是C++11的特性。  
  
(4)算法  
遍历元素 //略  
元素翻转  
#include <algorithm>  
reverse(vec.begin(), vec.end());  
  
元素排序  
#include <algorithm>  
sort(vec.begin(), vec.end()); //采用的是从小到大的排序  
//如果想从大到小排序，可以采用上面反转函数，也可以采用下面方法:  
bool Comp(const int& a, const int& b) {  
return a > b;  
}  
sort(vec.begin(), vec.end(), Comp);

二模拟建树过程：

1\. 定义结构体内部有两元素，一个代表节点标号id，一个代表权值wi

2\. 定义 结构体类型的vector不定长数组 vector<node>V[999];

3.以v的下表作为父节点，将不定长数组vector扩张，得到模拟的树

3.题意可知从根节点开始，到所有节点的最短路，利用 dfs 进行深度遍历

三：题意分析

要点由于可以跨级传送级（a到b到c的情况下，可以利用传送直接到c）

首选利用 分治的思想 可以把 多层跨级认为三层跨级  

所以 所有选择的情况如下：

a b c  

X--------------->Y-------------->Z

m n

  

解释 在X Y 出传送的花费为a b， X->Y Y->Z 路径的花费为 m n。

二层传递下只需要比较 传送与路径值的大小就好

三层传递下  

b[y]+min(b,n);

a(a+b,a+n 在权值没有负值的情况下一定大于a)

所以三层传递的最小值是min（a，shotr[y]+min(b,n)）;

利用vector数组进行操作的时候，我们是不能在x点下，对z点进行处理的（只能处理离x最近的y），对上述操作进行进一步思考

对Y点来说他传送的费用是 short[y]+b，但是这个值可能比从a出传送贵（a>m 但是 a<m+b）所以此时更新从b出的传送价格为a

代码如下：

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <vector>
    #include <algorithm>
    #define inf 0x3f3f3f3f
    using namespace std;
    struct node
    {
        int id;//存标号
        int wi;//存路径权值
    }h;
    vector<node>v[120000];
    int n;
     int a[120000];//存传送费用
     int b[120000];//存到每个点的最小值
    void dfs(int x, int tp)
    {
       for(int i=0; i<v[x].size(); i++)
       {
         int id=v[x][i].id;
         int wi=v[x][i].wi;
         int  w=b[x]+wi;//w 代表到上一个点的最短距离加上路径权值
         b[id]=min(tp,w); //tp代表从上一个点传送的最小值
         int t=min(tp,b[id]+a[id]);//tp 表示从x点传送的最小值， b[id]+a[id]表示从id点开始传送的初始花费，来更新从id点开始传送的最小花费
         dfs(id,t);
       }
    }
    int main ()
    {
        while(~scanf("%d",&n))
        {
            for(int i=0;i<n;i++)//清空不定长数组
            v[i].clear();
            for(int i=1;i<=n;i++)
            {
                scanf("%d",&a[i]);
            }
            for(int i=2;i<=n;i++)
            {
                int j;
                int k;
                scanf("%d %d",&j,&k);
                h.id=i;
                h.wi=k;
                v[j].push_back(h);
            }
            b[1]=0;
            dfs(1,a[1]);
            for(int i=1; i<=n;i++)
            {
                printf("%d ",b[i]);
            }
            printf("\n");
        }
        return 0;
    }
    

  
  

  

  

