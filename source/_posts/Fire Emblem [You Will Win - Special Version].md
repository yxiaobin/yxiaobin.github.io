---
title: Fire Emblem [You Will Win - Special Version]
date: 2017-05-15 17:25:03
categories: 数据结构文章标签
---
####  Problem Description

火焰之纹章 (Fire Emblem) 是 SRPG 游戏的巅峰之作，其严格的战场设定和复杂的战斗和剧情系统，使得游戏的难度相当高。  
从 1990 年至今，游戏共在各个游戏平台推出了十多部作品，都相当的受欢迎。

![3744](http://acm.sdut.edu.cn/image/3744.png)

我们来简化一下游戏系统，bLue<!-- more --> 和 Stone 两人对战，每人有攻（初始攻击力）、防（初始防御力）、速（初始攻击速度）、血（生命值）4
个属性，并且都会携带一把武器和一件防具。

武器有 2 种属性：攻击力加成和重量。

防具有 2 种属性：防御力加成和重量。

玩家的实际攻击力 = 初始攻击力 + 武器攻击力加成。

玩家的实际防御力 = 初始防御力 + 防具防御力加成。

玩家的实际攻击速度 = 初始攻击速度 - 武器重量 - 防具重量。

玩家可用的武器和防具及其属性如下表（允许双方使用相同的武器和防具）：

类型  |  名称  |  属性加成  |  重量  
---|---|---|---  
武器  |  DevineRapier  |  10  |  5  
武器  |  InfinityBlade  |  25  |  25  
武器  |  TheSwordOfPBH  |  50  |  10  
防具  |  Immortal  |  15  |  5  
防具  |  Ragnarok  |  25  |  25  
防具  |  HuaJiShield  |  50  |  1  
  
当游戏开始时，两人  轮流  发起战斗（如果某人的攻击速度小于等于 0 ，则他将无法发起战斗），每场战斗的规则为：  
攻方先攻击一次，守方接着再攻击一次。攻击速度快的人可以在本轮战斗结束时额外再攻击一次（攻击速度相等时不存在额外攻击）。

伤害计算公式：伤害 = 自己的攻击力 - 对方的防御力（伤害小于等于 0 时均视为 0）。

在任何一次攻击结束后，如果被攻击者的生命值小于等于 0，则他将立即输掉游戏。

鉴于游戏的设定为蓝方先手，那么 bLue 当然要先攻击了。我们的问题就是，他们两人究竟谁会获得胜利呢？

####  Input

输入数据有多组（数据组数不超过 100），到 EOF 结束。  
每组输入两行数据：

  * 第一行输入 4 个整数和 2 个字符串，分别代表 bLue 的攻、防、速、血、武器、防具； 
  * 第二行输入 4 个整数和 2 个字符串，分别代表 Stone 的攻、防、速、血、武器、防具。 

所有整数数值都在 [1, 100] 范围内，字符串不含空格且长度最大为 13 。

####  Output

每组输出占一行，若 bLue 赢，输出 "bLue wins!"；若 Stone 赢，输出 "Stone
wins!"；若无法分出胜负（两人都无法发动战斗或两人都无法对对方造成伤害），则输出 "bLue Stone have to give
up!"（输出均不包含引号）。

####  Example Input

    
    
    30 5 25 30 DevineRapier Immortal
    20 5 40 30 DevineRapier Ragnarok
    

####  Example Output

    
    
    bLue wins!

####  Hint

对第 1 组示例的解释：

bLue 的属性为：攻击力：40，防御力：20，攻击速度：15，可以造成的伤害：10。  
Stone 的属性为：攻击力：30，防御力：30，攻击速度：10，可以造成的伤害：10。

bLue 的攻击速度高，所以他每轮战斗结束时都会额外攻击一次。

战斗过程（b 表示 bLue，S 表示 Stone，→ 表示攻击，hp1 表示 bLue 的生命值，hp2 表示 Stone 的生命值）：

Battle 1:

b→S hp2: 30-10=20  
S→b hp1: 30-10=20  
b→S hp2: 20-10=10（额外攻击）

Battle 2:

S→b hp1: 20-10=10  
b→S hp2: 10-10=0

对于本题输入输出中所涉及的字符串，建议将其复制粘贴到你的代码中，以避免拼写错误。

**总体不难 是一个小型的模拟就是坑点有点多**

**坑点总结如下（可能不全）：**

**1\. 攻速小于等于0的情况下不攻击。**

**2\. 当一方攻速为0另一方攻速不为0但是攻击为0的情况下也是平局。**

**3.无论谁攻速快都是blue先攻击。**

**4.没攻击一次都要判断一下是否空血了。**

**5.攻击有顺序，不能允许攻击快的连续攻击两次。**

**6\. 攻击小于等于0，攻速小于等于0 ，均为0（即为小于0下强制等于0）**

    
    
    #include <stdio.h>
    #include <string.h>
    #include <algorithm>
    using namespace std;
    struct node
    {
        int g;
        int f;
        int su;
        int xie;
        char wu[150];
        char jv[150];
    } zxzc;
    int main ()
    {
        struct node x,y;
        int ax,bx,cx,dx,ay,by,cy,dy,j,k;
        while (~scanf("%d %d %d %d %s %s",&x.g, &x.f, &x.su, &x.xie, x.wu, x.jv) )
        {
            scanf("%d %d %d %d %s %s",&y.g, &y.f, &y.su, &y.xie, y.wu, y.jv);
            if(strcmp(x.wu,"DevineRapier")==0)
            {
                ax=10;
                bx=5;
            }
            if(strcmp(x.wu,"InfinityBlade")==0)
            {
                ax=25;
                bx=25;
            }
            if(strcmp(x.wu,"TheSwordOfPBH")==0)
            {
                ax=50;
                bx=10;
            }
    
            if(strcmp(y.wu,"DevineRapier")==0)
            {
                ay=10;
                by=5;
            }
            if(strcmp(y.wu,"InfinityBlade")==0)
            {
                ay=25;
                by=25;
            }
            if(strcmp(y.wu,"TheSwordOfPBH")==0)
            {
                ay=50;
                by=10;
            }
    
            if(strcmp(x.jv,"Immortal")==0)
            {
                cx=15;
                dx=5;
            }
            if(strcmp(x.jv,"Ragnarok")==0)
            {
                cx=25;
                dx=25;
            }
            if(strcmp(x.jv,"HuaJiShield")==0)
            {
                cx=50;
                dx=1;
            }
            if(strcmp(y.jv,"Immortal")==0)
            {
                cy=15;
                dy=5;
            }
            if(strcmp(y.jv,"Ragnarok")==0)
            {
                cy=25;
                dy=25;
            }
            if(strcmp(y.jv,"HuaJiShield")==0)
            {
                cy=50;
                dy=1;
            }
            x.g=x.g+ax;
            x.f=x.f+cx;
            x.su=x.su-bx-dx;
            if(x.su<=0) x.su=0;
            y.g=y.g+ay;
            y.f=y.f+cy;
            y.su=y.su-by-dy;
            if(y.su<=0) y.su=0;
            int n,m;
            j=x.g-y.f;
            k=y.g-x.f;
            if(j<=0) j=0;
            if(k<=0) k=0;
            if(x.su==0 && y.su!=0)
            {
                if(k!=0)
                printf("Stone wins!\n");
                else printf("bLue Stone have to give up!\n");
    
            }
            else   if(x.su!=0 && y.su==0)
            {
                if(j!=0)
                printf("bLue wins!\n");
                else
                    printf("bLue Stone have to give up!\n");
            }
            else  if(x.su==0 && y.su==0) printf("bLue Stone have to give up!\n");
            else
            {
                if(x.su>y.su)
                {
                    if(j==0 && k==0)  printf("bLue Stone have to give up!\n");
                    else  if(j==0 && k!=0)  printf("Stone wins!\n");
                    else  if(j!=0 && k==0)  printf("bLue wins!\n");
                    else  if(j!=0 && k!=0)
                    {
                        while (1)
                        {
                            y.xie-=j;
                            if(y.xie<=0 && x.xie>0)
                            {
                                printf("bLue wins!\n");
                                break;
                            }
                            x.xie-=k;
                            if(x.xie<=0 && y.xie>0)
                            {
                                printf("Stone wins!\n");
                                break;
                            }
                            y.xie-=j;
                            if(y.xie<=0 && x.xie>0)
                            {
                                printf("bLue wins!\n");
                                break;
                            }
                            if(y.xie<=0 && x.xie<=0)
                            {
                                printf("bLue Stone have to give up!\n");
                                break;
                            }
                        }
                    }
    
                }
                else if(x.su<y.su)
                {
                    if(j==0 && k==0)  printf("bLue Stone have to give up!\n");
                    else    if(j==0 && k!=0)  printf("Stone wins!\n");
                    else    if(j!=0 && k==0)  printf("bLue wins!\n");
                    else    if(j!=0 && k!=0)
                    {
                        while (1)
                        {
                            y.xie-=j;
                            if(y.xie<=0 && x.xie>0)
                            {
                                printf("bLue wins!\n");
                                break;
                            }
                            x.xie-=k;
                            if(x.xie<=0 && y.xie>0)
                            {
                                printf("Stone wins!\n");
                                break;
                            }
                            x.xie-=k;
                            if(x.xie<=0 && y.xie>0)
                            {
                                printf("Stone wins!\n");
                                break;
                            }
                            if(y.xie<=0 && x.xie<=0)
                            {
                                printf("bLue Stone have to give up!\n");
                                break;
                            }
                        }
                    }
                }
                else
                {
                    if(j==0 && k==0)  printf("bLue Stone have to give up!\n");
                    else   if(j==0 && k!=0)  printf("Stone wins!\n");
                    else     if(j!=0 && k==0)  printf("bLue wins!\n");
                    else     if(j!=0 && k!=0)
                    {
                        while (1)
                        {
                            y.xie-=j;
                            if(y.xie<=0 && x.xie>0)
                            {
                                printf("bLue wins!\n");
                                break;
                            }
                            x.xie-=k;
                            if(x.xie<=0 && y.xie>0)
                            {
                                printf("Stone wins!\n");
                                break;
                            }
                            if(y.xie<=0 && x.xie<=0)
                            {
                                printf("bLue Stone have to give up!\n");
                                break;
                            }
                        }
                    }
                }
    
    
            }
        }
    }
    

  
  

