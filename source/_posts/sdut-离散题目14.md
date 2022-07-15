---
title: sdut-离散题目14
date: 2017-05-27 00:08:52
categories: 离散数学文章标签
---
  
离散题目14  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
判断集合是不是对称的。  
Input  
  
首先输入两个数n，m表示集合中元素的个数，以及存在的关系数。  
接下来1行包含n个以空格分隔的整数。  
接下来m行，每行包含两个数a，b表示关系。 <!-- more --> 
（1< = n < = 1000,1 < = a,b < = n,m < = n*(n-1)&& m < = 1000）  
Output  
  
对于每组输入，如果这个集合是对称的则输出“YES”，否则输出“NO”。（均不包含引号）  
Example Input  
  
5 8  
1 1  
1 2  
2 1  
3 3  
2 3  
3 2  
4 5  
5 4  
5 9  
1 1  
1 2  
2 1  
3 3  
2 3  
3 2  
4 5  
5 4  
5 1  
Example Output  
  
YES  

NO

提示： 双层for 循环下面， 如果ij存在 判断 是否ji存在就可以了，还有 多组输入，学长不走心，没有说明白

    
    
    #include <stdio.h>
    #include <string.h>
    #include <algorithm>
    using namespace std;
    int map[1300][1300];
    int a[1300];
    int b[1300];
    int n,m;
    int main ()
    {
        int i,j,k;
       while (~scanf("%d %d",&n,&m) )
       {
            memset(map,0,sizeof(map));
            for(i=0;i<m;i++)
            {
                scanf("%d %d",&j,&k);
                map[j][k]=1;
                a[i]=j;
                b[i]=k;
    
            }
            int flag=0;
            for(i=0; i<m; i++)
            {
                for(j=0; j<m; j++)
                {
                    if(map[a[i]][b[i]]==1)
                    {
                        if(map[b[i]][a[i]]==0)
                        {
                            flag=1;
                            break;
                        }
                    }
                }
            }
            if(flag==1) printf("NO\n");
            else   printf("YES\n");
            }
    
    
    }
    

  
  

