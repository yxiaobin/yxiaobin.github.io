---
title: sdut-l离散题目2
date: 2017-05-26 23:09:42
categories: 离散数学文章标签
---
DaYu是一个喜欢看电影的好孩子，他的电脑里有成千上万部电影。因为某些不可描述的原因，他把这些电影以互不相同的编号命名(编号是数字且范围在(0,1000000)之间)。因为电影实在太多，他记不住自己已经看过了哪些电影。现在他把他看电影的记录给你，请你帮他检查一下他有没有看重复的电影。如果没有，输出“true”，否则输出“false”。  
Input  
  
第一行输入组数T(T<1000),每<!-- more -->组的第一行输入他看的电影数量n(0 < n < 1000000)，第二行输入n个数字，分别是每一部电影的编号。  
Output  
  
对于每组数据，如果没有重复的，那么输出true，否则输出false。  
Example Input  
  
2  
5  
1 2 3 4 5  
5  
1 2 3 4 4  
Example Output  
  
true  

false

提示：首选可以开出a【n】大的数组的 ， 然后所有的值都是大于0的，和离散题目1一样，采用数组下标存的方式就可以了。

    
    
    #include <stdio.h>
    #include <string.h>
     int a[1000100];
    int main ()
    {
    
        int t, x,i,n;
        scanf("%d",&t);
        while(t--)
        {
            memset(a,0,sizeof(a));
            scanf("%d",&n);
            for(i=1;i<=n;i++)
            {
                scanf("%d",&x);
                a[x]++;
            }
            int flag=0;
            for(i=1;i<=n;i++)
            {
                if(a[i]>1)
                {
                    flag=1;
                    break;
                }
            }
            if(flag==1) printf("false\n");
            else printf("true\n");
        }
        return 0;
    }
    

  
  

