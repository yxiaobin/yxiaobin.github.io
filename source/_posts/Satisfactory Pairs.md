---
title: Satisfactory Pairs
date: 2017-06-25 18:46:07
categories: 数据结构
---
Given a positive integer, , find and print the number of pairs of positive
integers , where , that exist such that the equation (where and are positive
integers) has at least one solution.  
  
Input <!-- more -->Format  
  
A single positive integer denoting .  
  
Constraints  
  
Output Format  
  
Print a single integer denoting the number of such pairs.  
  
Sample Input 0  
  
4  
  
Sample Output 0  
  
2  
  
Explanation 0  
  

There are two such pairs: and .

题意：给出一个n，找出(a, b) a<b的个数，且 ax + by == n。

这道题连着两次训练赛中出现，却一直没有去解决，在这个大周天的时间狠下心来把这个题目给补掉。

思路 枚举 a == i, 从 1 到 n/2，然后枚举 x，即 ax = i * j,这个必须满足i * j < n
才行，所以虽然看上去2层for循环其实复杂度是 1/x 从1到n积分，复杂度 nln(n)

然后对于每个ij，扫一遍已经预处理出的vector[n - i*j]，如果对于当前i，这个元素vector[n - i*j][k] 大于i
且没有被标记为i(即对于当前a == i时，这个b还没有出现过)，就ans++，然后标记为 f[..] = i;

    
    
    #include <iostream>
    #include <cstdio>
    #include <cmath>
    #include <vector>
    #include <algorithm>
    #include <cstring>
    using namespace std;
    typedef long long LL;
    const int maxn = 3e5 + 8;
    
    vector<int> s[maxn];
    int f[maxn];
    int main()
    {
    
        int n, ans = 0;
        LL i, j, k, t;
        cin >> n;
    
        for(i = 1; i < n; i++)
        {
            for(j = i; j < n; j++)
            {
                if(i * j >= n) break;
                s[i*j].push_back(i);
                if(i != j)
                {
                    s[i*j].push_back(j);
                }
            }
        }
        int sz;
        for(i = 1; i <= n/2; i++)
        {
            for(j = 1; j < n; j++)
            {
                if(i * j >= n) break;
                t = n - i * j;
                if(t <= i) break;
                sz = s[t].size();
                for(k = 0; k < sz; k++)
                {
    
                    if(s[t][k] > i && f[s[t][k]] != i)
                    {
    
                        f[s[t][k]] = i;
                        ans++;
                    }
                }
            }
        }
    
        printf("%d\n", ans);
    
        return 0;
    }
    

  
  

  

