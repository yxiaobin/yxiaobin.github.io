---
title: 昂贵的聘礼 POJ - 1062 ----对区间进行枚举的Dijst算法
date: 2017-08-04 09:26:44
categories: 数据结构文章标签
---
昂贵的聘礼  
Time Limit: 1000MS Memory Limit: 10000K  
Total Submissions: 50284 Accepted: 15061  
  
Description  
年轻的探险家来到了一个印第安部落里。在那里他和酋长的女儿相爱了，于是便向酋长去求亲。酋长要他用10000个金币作为聘礼才答应把女儿嫁给他。探险家拿不出这么多金币，便请求酋长降低要求<!-- more -->。酋长说："嗯，如果你能够替我弄到大祭司的皮袄，我可以只要8000金币。如果你能够弄来他的水晶球，那么只要5000金币就行了。"探险家就跑到大祭司那里，向他要求皮袄或水晶球，大祭司要他用金币来换，或者替他弄来其他的东西，他可以降低价格。探险家于是又跑到其他地方，其他人也提出了类似的要求，或者直接用金币换，或者找到其他东西就可以降低价格。不过探险家没必要用多样东西去换一样东西，因为不会得到更低的价格。探险家现在很需要你的帮忙，让他用最少的金币娶到自己的心上人。另外他要告诉你的是，在这个部落里，等级观念十分森严。地位差距超过一定限制的两个人之间不会进行任何形式的直接接触，包括交易。他是一个外来人，所以可以不受这些限制。但是如果他和某个地位较低的人进行了交易，地位较高的的人不会再和他交易，他们认为这样等于是间接接触，反过来也一样。因此你需要在考虑所有的情况以后给他提供一个最好的方案。  
为了方便起见，我们把所有的物品从1开始进行编号，酋长的允诺也看作一个物品，并且编号总是1。每个物品都有对应的价格P，主人的地位等级L，以及一系列的替代品Ti和该替代品所对应的"优惠"Vi。如果两人地位等级差距超过了M，就不能"间接交易"。你必须根据这些数据来计算出探险家最少需要多少金币才能娶到酋长的女儿。  
  
Input  
输入第一行是两个整数M，N（1 <= N <=
100），依次表示地位等级差距限制和物品的总数。接下来按照编号从小到大依次给出了N个物品的描述。每个物品的描述开头是三个非负整数P、L、X（X <
N），依次表示该物品的价格、主人的地位等级和替代品总数。接下来X行每行包括两个整数T和V，分别表示替代品的编号和"优惠价格"。  
  
Output  
输出最少需要的金币数。  
  
Sample Input  
  
1 4  
10000 3 2  
2 8000  
3 5000  
1000 2 1  
4 200  
3000 2 1  
4 200  
50 2 0  
  
Sample Output  
  

5250

  

这个题目的重点解决地方在于对地位的处理，不能跨越进行地位处理，我们可以暴力枚举所有满足范围的区间，然后找到最小值

  

    
    
    #include <iostream>
    #include<cstdio>
    #include <cstring>
    #include <cmath>
    #include <queue>
    #include <algorithm>
    #include <vector>
    #define inf 0x3f3f3f3f
    using namespace std;
    int map[150][150];
    int dist[150];
    int book[150];
    int vis[150];
    int n,m;
    int Dijst()
    {
        for(int i=1; i<=n; i++)
        dist[i]=map[0][i];
        for(int i=1; i<=n; i++)
        {
            int Min=inf;
            int Min_id=0;
            for(int j=1; j<=n; j++)
            {
                if(Min>dist[j]&& !vis[j] )
                {
                    Min=dist[j];
                    Min_id=j;
                }
            }
            if(Min_id==0)
            {
               break;
            }
            vis[Min_id]=1;
            for(int j=1; j<=n; j++)
            {
                if( dist[j]>dist[Min_id]+map[Min_id][j])
                {
                    dist[j]=dist[Min_id]+ map[Min_id][j];
                }
            }
    
        }
        return dist[1];
    }
    int main ()
    {
        while ( ~scanf("%d %d",&m,&n))
        {
            int p,l,x,a,b;
            memset(map,inf,sizeof(map));
            memset(dist,inf,sizeof(dist));
            for(int i=1; i<=n; i++)
            {
                scanf("%d %d %d",&p,&l,&x);
                map[0][i]=p;
                //dist[i]=p;
                book[i]=l;
                for(int j=0; j<x; j++)
                {
                    scanf("%d %d",&a,&b);
                    map[a][i]=b;
                }
            }
            int ans=9999999;
            for(int i=0;i<=m;i++)
            {
                 memset(vis,0,sizeof(vis)); //Wa好久，注意每进行一次区间选择的时候，你需要重新把vis全部清零
                for(int j=1;j<=n;j++)
                {
                    if(book[j]<book[1]-i || book[j]>book[1]+m-i)
                    /*假设 m为2， 那么 可以交易的区间范围为-2到2，但是这个的范围是4，远远大于等级限制2，所以需要进行区间枚举，-2～0 -1～1 0～2 枚举三次 */
                    vis[j]=1;
                }
                ans=min(ans,Dijst());
            }
            cout<<ans<<endl;
    
        }
    
        return 0;
    
    }
    

  
  

  

