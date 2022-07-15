---
title: 英语考试FZU（最小生成树）
date: 2017-07-27 10:57:05
categories: 数据结构文章标签
---
  
  
在过三个礼拜，YellowStar有一场专业英语考试，因此它必须着手开始复习。  
  
这天，YellowStar准备了n个需要背的单词，每个单词的长度均为m。  
  
YellowSatr准备采用联想记忆法来背诵这n个单词：  
  
1、如果YellowStar凭空背下一个新词T，需要消耗单词长度m的精力  
  
2、如果YellowSatr之前已经背诵了一些单词，它可以选择<!-- more -->其中一个单词Si，然后通过联想记忆的方法去背诵新词T，需要消耗的精力为hamming(Si,
T) * w。  
  
hamming(Si, T)指的是字符串Si与T的汉明距离，它表示两个等长字符串之间的汉明距离是两个字符串对应位置的不同字符的个数。  
  
由于YellowStar还有大量繁重的行政工作，因此它想消耗最少的精力背诵下这n个单词，请问它最少需要消耗多少精力。  
Input  
  
包含多组测试数据。  
  
第一行为n, m, w。  
  
接下来n个字符串，每个字符串长度为m，每个单词均为小写字母'a'-'z'组成。  
  
1≤n≤1000  
  
1≤m, w≤10  
Output  
  
输出一个值表示答案。  
Sample Input  
  
3 4 2  
abch  
abcd  
efgh  
  
Sample Output  
  
10  
  
Hint  
  

最优方案是：先凭空记下abcd和efgh消耗精力8,在通过abcd联想记忆去背诵abch，汉明距离为1,消耗为1 * w = 2,总消耗为10

。

把所有的单词全部标记为点，两个方法变成边，找最小生成树  

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    # define inf 0x3f3f3f3f;
    using namespace std;
    int map[1100][1100];
    int n,m,w;
    void Int()
    {
        for(int i=0;i<=n+1;i++)
        {
            for(int j=0;j<=n+1;j++)
            {
                map[i][j]=m;
            }
        }
    }
    void prim()
    {
        int book[1200];
        int edge[1200];
        memset(book,0,sizeof(book));
        for(int i=1;i<n;i++)
        {
          edge[i]=map[0][i];
        }
        book[0]=0;
        int sum=m;
        for(int i=1;i<n;i++)
        {
            int min=inf;
            int minid=0;
            for(int j=1;j<n;j++)
            {
                if(!book[j] && min>edge[j])
                {
                    min=edge[j];
                    minid=j;
                }
            }
            sum+=min;
            book[minid]=1;
            for(int j=1;j<n;j++)
            {
                if(map[minid][j]<edge[j])
                {
                    edge[j]=map[minid][j];
                }
            }
        }
        printf("%d\n",sum);
    
    }
    int haming(char s[],char v[])
    {
        int sum=0;
        for(int i=0;i<m;i++)
        {
            if(s[i]!=v[i])
            {
                sum++;
            }
        }
        return sum*w;
    }
    
    int main ()
    {
        char s[1200][12];
        while(cin>>n>>m>>w)
        {
            Int();
            for(int i=0;i<n;i++)
            {
                scanf("%s",s[i]);
            }
            for(int i=0;i<n;i++)
            {
                for(int j=i+1;j<n;j++)
                {
                    int sum=haming(s[i] , s[j]);
                    if(sum<map[i][j] )
                    {
                        map[i][j]=sum;
                        map[j][i]=sum;
                    }
                }
            }
            prim();
        }
        return 0;
    }
    

  

