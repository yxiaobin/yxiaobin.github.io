---
title: sdut- 离散题目4
date: 2017-05-26 23:24:35
categories: 离散数学文章标签
---
离散题目4  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
题目给出两个非空整数集，请写出程序求两个集合的交集。  
Input  
  
多组输入，每组输入包括两行，第一行为集合A的元素，第二行为集合B的元素。具体参考示例输入。 每个集合元素个数不大于3000，每个元<!-- more -->素的绝对值不大于2^32
- 1。  
Output  
  
每组输入对应一行输出，为A、B的交集，如果交集为空输出"NULL"，否则交集的元素按递增顺序输出，每个元素之间用空格分割。  
Example Input  
  
1 2 3 4 5  
1 5 3 6 7  
1 2 4 5 3  
6 7 8 9 10  
Example Output  
  
1 3 5  

NULL

提示 ： 由于没有标明每一个集合有几个元素，最容易想到的办法就是切割字符串（实际上最简单的是 c++的
输入流，可是我目前不会…………），但是切割字符串很麻烦，具体方法，看代码。

将数组开的小了回报RE的错误

由于后台在Windows上生成的数据，每一行后面有一个 \n \t ， 因此，你需要读字符串少读一个

    
    
    #include <stdio.h>
    #include <string.h>
    #include <algorithm>
    # define max1 999999
    
    using namespace std;
    char  a[max1];
    char  b[max1];
    long long int   c[max1];
    long long int   d[max1];
    long long int   g[max1];
    int main ()
    {
        while (gets(a)!=NULL)
        {
            gets(b);
            int flag,n,m,i,j,k,x;
            n=strlen(a);
            flag=0;
            int cx=0;
            x=0;
            k=1;
            for(i=n-2; i>=0; i--)
            {
                if(a[i]==' ')
                {
                    x=0;
                    k=1;
                }
                if(a[i]!=' ')
                {
                    if(a[i]>='0' && a[i]<='9')
                    {
                        x=x+(a[i]-'0')*k;
                        k=k*10;
                    }
                    if(a[i]=='-')
                    {
                        x=-x;
                    }
                    if(a[i-1]==' ' || i-1==-1)
                    {
                        c[cx]=x;
                        cx++;
                    }
                }
    
            }
            m=strlen(b);
            int dx=0;
            x=0;
            k=1;
            for(i=m-2; i>=0; i--)
            {
                if(b[i]==' ')
                {
                    x=0;
                    k=1;
                }
                if(b[i]!=' ')
                {
                    if(b[i]>='0' && b[i]<='9')
                    {
                        x=x+(b[i]-'0')*k;
                        k=k*10;
                    }
                    if(b[i]=='-')
                    {
                        x=-x;
                    }
                    if(b[i-1]==' ' || i-1==-1)
                    {
                        d[dx]=x;
                        dx++;
                    }
                }
            }
            int ex=0;
            for(i=0; i<cx; i++)
            {
                for(j=0; j<dx; j++)
                {
                    if(c[i]==d[j])
                    {
                         g[ex]=c[i];
                         ex++;
                         flag=1;
                         break;
                    }
                }
            }
    
    
            /* 测试样例输出
            for(i=0;i<cx;i++)
            {
                printf("%lld ",c[i]);
            }
            printf("\n");
            for(i=0;i<dx;i++)
            {
                printf("%lld ",d[i]);
            }
            printf("\n");
            for(i=0;i<ex;i++)
            {
                printf("%lld ",g[i]);
            }
            printf("\n");
            测试样例输出结束*/
    
    
            if(flag==0) printf("NULL\n");
            else
            {
                sort(g,g+ex);
                for(i=0; i<ex; i++)
                {
                    printf("%lld%c",g[i],i==ex-1?'\n':' ');
                }
            }
        }
        return 0;
    }
    

  

