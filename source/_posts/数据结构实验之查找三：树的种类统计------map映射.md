---
title: 数据结构实验之查找三：树的种类统计------map映射
date: 2017-08-17 10:13:54
categories: 数据结构
---
####  Problem Description

随着卫星成像技术的应用，自然资源研究机构可以识别每一个棵树的种类。请编写程序帮助研究人员统计每种树的数量，计算每种树占总数的百分比。

####  Input

输入一组测试数据。数据的第1行给出一个正整数N (n <=
100000)，N表示树的数量；随后N行，每行给出卫星观测到的一棵树的种类名称，树的名称是一个不超过20个字符的字符串，字符<!-- more -->串由英文字母和空格组成，不区分大小写。

####  Output

按字典序输出各种树的种类名称和它占的百分比，中间以空格间隔，小数点后保留两位小数。

####  Example Input

    
    
    2
    This is an Appletree
    this is an appletree

####  Example Output

    
    
    this is an appletree 100.00%

####  思路：

把所有的字符串利用map函数映射为一个数值，利用桶排的思维，统计一下每一个数值出现的个数，最后冒泡按字典序排序即可

    
    
    #include<iostream>
    #include<cstring>
    #include<cstdio>
    #include <map>
    #include<algorithm>
    using namespace std;
    map<int,string>mp; // 整形到字符串的映射
    int a[100100];
    char s[100];
    void become(int n)//手写的字母转换
    {
        for(int i=0;i<n;i++)
        {
            if(s[i]>='A' && s[i]<='Z')
            {
                s[i]=s[i]-'A'+'a';
            }
        }
    }
    int main ()
    {
        int n;
        scanf("%d",&n);
        getchar();
        memset(a,0,sizeof(a));
        int px=0;
        for(int i=0;i<n;i++)
        {
            gets(s);
            int m=strlen((s));
            become(m);
            int flag=0;
            for(int i=0;i<px;i++)
            {
                if(mp[i]==s)
                {
                    flag=1;
                    a[i]++;
                    break;
                }
            }
            if(!flag)//表示当前已存的mp里面没有该字符串
            {
                mp[px]=s;
                a[px]++;
                px++;
            }
        }
        string t;
        int k;
        for(int i=0; i<px-1;i++)
        {
            for(int j=i+1;j<px;j++)
            {
                if(mp[j]<mp[i])//按照字典序换序
                {
                    t=mp[i];
                    mp[i]=mp[j];
                    mp[j]=t;
                    k=a[i];
                    a[i]=a[j];
                    a[j]=k;
                }
            }
        }
        for(int i=0;i<px;i++)
        {
        cout<<mp[i]<<" ";
        a[i]*=100;
        printf("%.2lf%%\n",(double)a[i]/n);
        }
    }
    

  
  

  

