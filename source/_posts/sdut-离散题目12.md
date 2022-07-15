---
title: sdut-离散题目12
date: 2017-05-26 23:52:42
categories: 离散数学文章标签
---
离散题目12  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
给出两个集合，以及两个集合上的关系。判断该关系能不能构成函数  
Input  
  
多组输入。第一行数字表示集合A；第二行数字表示集合B；第三行一个数字N，表示关系的个数。以下N行，每行两个数字a b，用<!-- more -->来描述关系a→b。0 < n < =
20000,集合A、B的大小不超过10000.  
Output  
  
每组数据输出一行，所给关系属于函数，输出’yes’ ，否则输出‘no’。  
Example Input  
  
1 2 3  
4 5 6  
3  
1 4  
2 5  
3 6  
1 2 3  
4 5 6  
3  
1 4  
1 5  
1 6  
Example Output  
  
yes  

no

坑点 ：使用了 c++ 的集合函数，还有 要多吃空格……

    
    
    #include<bits/stdc++.h>
    using namespace std;
    char s[25000];
    int main()
    {
        set<int> a, b;
        set<int>::iterator it;
        int n, len, i;
        while(gets(s))
        {
            len = strlen(s);
            for(i = 0; i < len; i++)
            {
                if(s[i] >= '0' && s[i] <= '9')
                {
                    a.insert(s[i] - '0');
                }
            }
            gets(s);
            len = strlen(s);
            for(i = 0; i < len; i++)
            {
                if(s[i] >= '0' && s[i] <= '9')
                {
                    b.insert(s[i] - '0');
                }
            }
            scanf("%d", &n);
            int num1, num2;
            map<int, int> c;
            int flag = 0;
            for(i = 0; i < n; i++)
            {
                scanf("%d %d", &num1, &num2);
                if(!c.count(num1))
                {
                    c[num1] = num2;
                }
                else {
                    if(c[num1] != num2)
                        flag = 1;
                }
            }
            gets(s);
            if(!flag) printf("yes\n");
            else printf("no\n");
            a.clear(), b.clear(); c.clear();
        }
        return 0;
    }

  
  

