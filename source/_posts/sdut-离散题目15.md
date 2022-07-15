---
title: sdut-离散题目15
date: 2017-05-27 00:15:38
categories: 离散数学文章标签
---
  
离散题目15  
Time Limit: 1000MS Memory Limit: 65536KB  
Submit Statistic  
Problem Description  
  
给出集合X、X上的关系R，判断关系R是不是传递的。  
例如： A={1,2,3} , R={<1,1>,<1,2>,<2,1>,<3,3>,<2,3>,<3,2>, <2,2>,<1,3>,<3,1><!-- more -->}
显然，R具有传递性。  
Input  
  
多组输入，每组输入第一行为集合X的元素；第二行为一个整数n ( n > 0
)，代表X上的关系R中序偶的个数；接下来n行用来描述X上的关系R，每行两个数字，表示关系R中的一个序偶。细节参考示例输入。  
非空集合X的元素个数不大于500，每个元素的绝对值不大于2^32 - 1。  
Output  
  
每组输入对应一行输出，如果关系R具有传递性输出 ”true”，否则输出 ”yes”。  
Example Input  
  
1 2 3  
9  
1 1  
2 2  
3 3  
1 2  
2 1  
1 3  
3 1  
2 3  
3 2  
1 2 3  
6  
1 1  
1 2  
3 3  
2 3  
3 2  
2 2  
Example Output  
  
true  

yes

提示： 数据可能存在负的而且很大，所以，数组存下表不行了，于是乎采用机构体存x，y 然后 若a.y=b.x 那么看看 有没有一个c 满足 c.x=a.x
c.y=b.y ，如果全部都满足那输出就好了

    
    
    #include <iostream>
    #include <stdio.h>
    #include <string.h>
    #include <sstream>
    using namespace std;
    struct node
    {
        int x;
        int y;
    } b[999];
    int main()
    {
        int m,i,j,k;
        string line;
        int flag;
        while (getline(cin,line))
        {
            scanf("%d",&m);
            for (i=0; i<m; i++)
            {
                scanf("%d %d",&b[i].x,&b[i].y);
            }
            getchar();
            getchar();
            flag=1;
            for(i=0; i<m; i++)
            {
                for(j=0; j<m; j++)
                {
                    if(b[j].x== b[i].y)
                    {
                        for(k=0; k<m; k++)
                        {
                            if(b[k].x==b[i].x && b[k].y==b[j].y)
                            {
                                break;
                            }
                        }
                        if(k==m) flag=0;
                    }
                }
            }
            if(flag==1 ) printf("true\n");
            else   printf("yes\n");
        }
        return 0;
    }
    

  
  

