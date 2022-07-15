---
title: Cash Machine  -----多重背包
date: 2017-08-12 19:51:49
categories: 数据结构
---
Description  
A Bank plans to install a machine for cash withdrawal. The machine is able to
deliver appropriate @ bills for a requested cash amount. The machine uses
exactly N distinct bill denominati<!-- more -->ons, say Dk, k=1,N, and for each
denomination Dk the machine has a supply of nk bills. For example,  
  
N=3, n1=10, D1=100, n2=4, D2=50, n3=5, D3=10  
  
means the machine has a supply of 10 bills of @100 each, 4 bills of @50 each,
and 5 bills of @10 each.  
  
Call cash the requested amount of cash the machine should deliver and write a
program that computes the maximum amount of cash less than or equal to cash
that can be effectively delivered according to the available bill supply of
the machine.  
  
Notes:  
@ is the symbol of the currency delivered by the machine. For instance, @ may
stand for dollar, euro, pound etc.  
  
Input  
The program input is from standard input. Each data set in the input stands
for a particular transaction and has the format:  
  
cash N n1 D1 n2 D2 ... nN DN  
  
where 0 <= cash <= 100000 is the amount of cash requested, 0 <=N <= 10 is the
number of bill denominations and 0 <= nk <= 1000 is the number of available
bills for the Dk denomination, 1 <= Dk <= 1000, k=1,N. White spaces can occur
freely between the numbers in the input. The input data are correct.  
  
Output  
For each set of data the program prints the result to the standard output on a
separate line as shown in the examples below.  
  
Sample Input  
  
735 3 4 125 6 5 3 350  
633 4 500 30 6 100 1 5 0 1  
735 0  
0 3 10 100 10 50 10 10  
  
Sample Output  
  
735  
630  
0  
0  
  
Hint  
The first data set designates a transaction where the amount of cash requested
is @735. The machine contains 3 bill denominations: 4 bills of @125, 6 bills
of @5, and 3 bills of @350. The machine can deliver the exact amount of
requested cash.  
  
In the second case the bill supply of the machine does not fit the exact
amount of cash requested. The maximum cash that can be delivered is @630.
Notice that there can be several possibilities to combine the bills in the
machine for matching the delivered cash.  
  
In the third case the machine is empty and no cash is delivered. In the fourth
case the amount of cash requested is @0 and, therefore, the machine delivers
no cash.  
  

Source

  

    
    
    #include <iostream>
    #include <cstring>
    #include <cstdio>
    #include <algorithm>
    using namespace std;
    int p[120000];
    int wi[12000];
    int num[120000];
    int dp[120000];
    int main ()
    {
        int n,m;
        while(~scanf("%d %d",&n,&m))
        {
            for(int i=0; i<m; i++)
            {
                scanf("%d %d",&p[i],&wi[i]);
            }
              memset(dp,0,sizeof(dp));
            for(int i=0;i<m;i++)
            {
                memset(num,0,sizeof(num));//每更换一次面额，计数器清零
                for(int j=wi[i];j<=n;j++)//对于第i种货币，其面额d[i]~cash间任一个状态都可能发生
                                        //num[j-w[i]]<p[i]
                {
                    if(dp[j]< dp[j-wi[i]]+wi[i] && num[j-wi[i]]<p[i])//取某种面额前，必须保证这次操作之前所取该种面额的次数小于p[i]
                    {
                        dp[j]=dp[j - wi[i]]+wi[i];//选取第i个物品后，背包容量（允许取的最大金额）减少w[i]
                        num[j]=num[j - wi[i]]+1;//对于当前状态j，第i种面额被抽了num[j]次
                    }
                }
            }
            cout<<dp[n]<<endl;
    
        }
        return 0;
    }
    

  
  

