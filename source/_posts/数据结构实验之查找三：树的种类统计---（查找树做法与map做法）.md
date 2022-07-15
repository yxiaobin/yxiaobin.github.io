---
title: 数据结构实验之查找三：树的种类统计---（查找树做法与map做法）
date: 2017-12-17 15:40:49
categories: 数据结构
---
随着卫星成像技术的应用，自然资源研究机构可以识别每一个棵树的种类。请编写程序帮助研究人员统计每种树的数量，计算每种树占总数的百分比。  
Input  
  
输入一组测试数据。数据的第1行给出一个正整数N (n <=
100000)，N表示树的数量；随后N行，每行给出卫星观测到的一棵树的种类名称，树的名称是一个不超过20个字符的字符串，字符串由英文字母和空格组成，不区分大小写。  
Output<!-- more -->  
  
按字典序输出各种树的种类名称和它占的百分比，中间以空格间隔，小数点后保留两位小数。  
Example Input  
  
2  
This is an Appletree  
this is an appletree  
Example Output  
  

this is an appletree 100.00%

  

看到这个题目的第一个想法就是利用map数组一一映射，由于测试不准谁用stl函数，先采用正常做法---加权二叉查找树的做法：

原理：由于按照字典序输出二叉树，因此这是一个基于字符串建立的树。

插入规则为，如果所插入的节点的字符串，在字符串比较函数strcmp（）中与根值root->name比较，较小的放到根的左孩子上，较大的放在右孩子上，，如果与根值相同，则根值的权值++；

代码如下：

    
    
    #include<algorithm>
    #include<iostream>
    #include<map>
    #include<cstdio>
    #include<cstring>
    using namespace std;
    struct node
    {
        char name[25]; //mingzi
        int num;//quanzhi
        struct node *lchild, *rchild;
    };
    struct node *creat(struct node *root,char s[])
    {
        if(!root)
        {
            root = new node;//不存在根节点，注意需要申请根节点，否则会CE
            strcpy(root->name,s);
            root->num=1;
            root->lchild =root->rchild =NULL;
        }
        else
        {
            if(strcmp(root->name,s)==0)
            {
                root->num++;
            }
            else  if(strcmp(root->name,s)>0)
            {
                root->lchild = creat(root->lchild, s);
            }
            else if(strcmp(root->name,s)<0)
            {
                root->rchild = creat(root->rchild, s);
            }
        }
        return root;
    };
    void  midprint(struct node *root, int n) //输出方式会 左孩子-根-右孩子 即中序遍历
    {
        if(root){
        midprint(root->lchild, n);
        printf("%s %.2lf%%\n",root->name, 100*(double)root->num/n);
        midprint(root->rchild, n);
        }
    }
    int main()
    {
        char s[25];
        int n;
       cin>>n;
    
            getchar();
            struct node *root;
            root = NULL;
            for(int j=0; j<n; j++)
            {
                gets(s);
                int m=strlen(s);
                //getsmall(s);
                for(int i=0; i<m; i++)
                {
                    if(s[i]>='A' && s[i]<='Z')
                        s[i]=s[i]-'A'+'a';
                }
               root = creat(root,s);
            }
            //lchild-root---rchild
            midprint(root, n);
    
    }

二：

利用 map函数映射 map<int string>mp 实现 字符串与数字的一一对应，实现 mp[1] = str1 mp[2] =str2……
如果来一个新的串strn 则将 mp[1]-mp[k]（一共k个）与之一一匹配，如果已包含这个串，则桶排计数函数num[x]++(when ->
map[x]==strn), 否则使得mp[k+1] =strn

这样完成后，利用冒泡排序对mp[i]数组进行一次从小到大的排序（注意num数组也要跟着变化）

然后输出即可，代码如下

    
    
    #include<iostream>
    #include<cstring>
    #include<cstdio>
    #include <map>
    #include<algorithm>
    using namespace std;
    map<int,string>mp;
    int a[100100];
    char s[100];
    void become(int n)
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
            if(!flag)
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
                if(mp[j]<mp[i])
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
    
    

  
  

