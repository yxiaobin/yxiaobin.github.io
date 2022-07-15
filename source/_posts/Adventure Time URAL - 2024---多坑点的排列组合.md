---
title: Adventure Time URAL - 2024---多坑点的排列组合
date: 2017-08-08 21:18:54
categories: 数据结构
---
  
‘Here’s for you!’ shouted Finn fighting the Shadow Guardians. ‘Jake! Collect
the Darkness Rocks and let’s run from here!’  
Jake would have been glad to finish as soon as possible, because it was w<!-- more -->et
and sad in the Dangerous Cave, but it was not so easy to gather Rocks. So he
called BMO and asked him to help with choosing an optimal set of Rocks. Jake
told BMO that there were n Rocks in the Cave, and they were numbered with
different integers from 1 to n. Each Rock was painted one of 26 colors. Jake
also reminded BMO of Princess Bubblegum’s warning: there should be at most k
Rocks of pairwise different colors among the Rocks taken from the Cave. Only a
set of Rocks with this property is safe. If one takes an unsafe set of Rocks
from the Cave, Cosmic Evil will be awakened! Of course, Jake doesn’t want to
awaken the Evil, but he wants to take as many Darkness Rocks from the Cave as
possible. Help BMO to find the size of the largest safe set of Rocks and the
number of different safe sets of this size. Two sets of Rocks are different if
one of them contains a Rock with a number that is not contained in the other
set.  
Input  
The first line contains n lowercase English letters (1 ≤ n ≤ 10 5); each
letter denotes the color of a Rock. In the second line you are given the
integer k (1 ≤ k ≤ 26).  
Output  
Output two integers separated with a space: the size of the largest safe set
of Darkness Rocks and the number of different safe sets of this size.  
Example  
input output  
  
abcde  
1  
  
  
  
1 5  
  
ababac  
2  
  
  
  

5 1

做题的时候注意一下几点

1\. 取石块的时候可以不连续

2\. 求组合数的时候 注意 c（m，n）=c（m，m-n），不然会爆掉

3\. k大于所给的字符串种类的时候，输出全部长度，且种类数为1

4\. 当最大的种类小于k的时候，假设加上第二大的数量大于k，注意把整个字符串第二大的数量全部统计完，从中取k-第一大的种类个，进行排列组合运算

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    char s[100100];
    int num[100100];//标记 每一个字符出现的个数-桶排
    long long int b[100100],bx; //标记每一个种类数出现的个数
    int cmp(int a, int b)
    {
        return a>b;
    }
    long long int f(int x, int y) //裸的排列组合计算
    {
        long long int a,b;
        a=1;
        b=1;
        if(y>x/2) //注意这种情况 不然的话，容易爆
        {
            y=x-y;
        }
        for(int i=y;i>=1;i--)
        {
            a=a*i;
        }
        for(int i=x;i>=x-y+1;i--)
        {
            b=b*i;
        }
        return b/a;
    }
    int main ()
    {
        int n;
        while(~scanf("%s %d",s,&n))
        {
            memset(num,0,sizeof(num));
            memset(b,0,sizeof(b));
            int len=strlen(s);
            for(int i=0; i<len; i++)
            {
                num[s[i]-'a']++; //统计字符串个数
            }
            sort(num,num+30,cmp);
            long long int Max=0;
            for(int i=0;i<n;i++)
            {
                Max+=num[i]; // 找到最大的max
            }
            for(int i=0; i<26; i++)
            {
                b[bx]++; 
                if(num[i]!=num[i+1])
                {
                     bx++;
                     if(num[i+1]==0)
                        break;
                }
            }
           long long  int ans=0;
           int flag=0;
            for(int i=0;i<bx;i++) // 找到什么情况下满足大于k个了，这个地方注意一定要吧满足大于k个的那个种类的数量全部找到，不要找到大于k的就break。
            {
                if(ans+b[i]>=n)
                {
                    int x=b[i];
                    int y=n-ans;
                    flag=1;
                    cout<<Max<<' '<<f(x,y)<<endl;
                    break;
                }
                else
                {
                    ans+=b[i];
                }
            }
            if(flag==0)
            printf("%d 1\n",len);
    
        }
        return 0;
    
    }
    

  
  

  

  

