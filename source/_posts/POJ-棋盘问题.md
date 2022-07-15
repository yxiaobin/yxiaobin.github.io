---
title: POJ-棋盘问题
date: 2017-05-18 22:22:25
categories: 数据结构文章标签
---
在一个给定形状的棋盘（形状可能是不规则的）上面摆放棋子，棋子没有区别。要求摆放时任意的两个棋子不能放在棋盘中的同一行或者同一列，请编程求解对于给定形状和大小的棋盘，摆放k个棋子的所有可行的摆放方案C。  
Input  
输入含有多组测试数据。  
每组数据的第一行是两个正整数，n k，用一个空格隔开，表示了将在一个n*n的矩阵内描述棋盘，以及摆放棋子的数目。 n <= 8 , k <= n  
<!-- more -->当为-1 -1时表示输入结束。  
随后的n行描述了棋盘的形状：每行有n个字符，其中 # 表示棋盘区域， . 表示空白区域（数据保证不出现多余的空白行或者空白列）。  
Output  
对于每一组数据，给出一行输出，输出摆放的方案数目C （数据保证C<2^31）。  
Sample Input  
2 1  
#.  
.#  
4 4  
...#  
..#.  
.#..  
#...  
-1 -1   
Sample Output  
2  

1

一些想法：

1\. 存字符，需要考虑到getchar（） 吃空格吃回车的问题。

2\. 模拟问题，进行dfs搜索。

3.. dfs搜索的思想：  从一个顶点  V  0  开始，
沿着一条路一直走到底，如果发现不能到达目标解，那就返回到上一个节点，然后从另一条路开始走到底。

4.由于每一个都不能同行同列，需要一个标记变量来标记已经确定的某行某列。

    
    
    #include <stdio.h>
    #include <string.h>
    #include <algorithm>
    using namespace std;
    int ha[10000];   //标记某一行
    int sum=0;
    int a[10][10];
    int n,m,i,j,k;
    void dfs(int fis, int num) // fis 表示 当前是第几行， num表示是需要几个
    {
        for(int j=0; j<n; j++) //从fis 行的第一列开始找
        {
            if(a[fis][j]==1 && ha[j]==0)
            {
                if(num==1)
                    sum++;
                else
                {
                    ha[j]=1;
                    for(int h=fis+1; h<n-num+2; h++) // 扣掉第fis 行开始找剩下的num-1个
                        dfs(h,num-1);
                    ha[j]=0;
                }
            }
        }
    }
    int main ()
    {
        char c;
        while (scanf("%d %d",&n,&m),n!=-1 &&m!=-1)
        {
             getchar ();
            sum=0;
            for(i=0; i<n; i++)
            {
                for(j=0; j<n; j++)
                {
                    scanf("%c",&c);
                    if(j==n-1)
                    {
                        getchar();
                    }
                    if(c=='#')
                    {
                        a[i][j]=1; // # 对应着数字1 而 . 对应着数字 0
                    }
                    else
                    {
                        a[i][j]=0;
                    }
                }
            }
            for(i=0; i<n; i++)
                ha[i]=0; //首选把每一行全部标记为0
            for(i=0; i<n; i++)
            {
                dfs(i,m); // 对每一行进行一遍dfs
            }
            printf("%d\n",sum);
        }
        return 0;
    }

  
  

  

