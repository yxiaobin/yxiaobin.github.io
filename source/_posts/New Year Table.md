---
title: New Year Table
date: 2017-06-06 22:50:59
categories: 数据结构文章标签
---
Gerald is setting the New Year table. The table has the form of a circle; its
radius equals R. Gerald invited many guests and is concerned whether the table
has enough space for plates for all those g<!-- more -->uests. Consider all plates to be
round and have the same radii that equal r. Each plate must be completely
inside the table and must touch the edge of the table. Of course, the plates
must not intersect, but they can touch each other. Help Gerald determine
whether the table is large enough for n plates.  
  
Input  
The first line contains three integers n, R and r (1 ≤ n ≤ 100, 1 ≤ r, R ≤
1000) — the number of plates, the radius of the table and the plates' radius.  
  
Output  
Print "YES" (without the quotes) if it is possible to place n plates on the
table by the rules given above. If it is impossible, print "NO".  
  
Remember, that each plate must touch the edge of the table.  
  
Example  
Input  
4 10 4  
Output  
YES  
Input  
5 10 4  
Output  
NO  
Input  
1 10 10  
Output  

YES

![](https://img-
blog.csdn.net/20170606224109463?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4MDY0ODEw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  

灵魂画家上线啦~

题意分析：大圆里面放最多的小圆，很明显小圆所有的边都相切，并且最外面的一层和大圆相切的时候放的最多啦~

此时 可以看出一个外接圆里面放一个正多边形，不过这个外接圆，应该是R-r
为半径的外接圆，这样的话，我们需要找到任意的同一条直径，在这个直径固定的一侧，可以放几个小的三角形
，每一个直角三角形对应一个圆。我们可以通过斜边与直角边的关系 找到 sina 但是我们需要求a 然后用360度除a 。

c++ 里面 用 反三角函数 是 acos asin 不是 arcsin arccos！！！ 并且返回的是
弧度，因此我们需要用π来除以我们得到的每一个小三角形对应的弧度课，但是π的取值我们也不是很确定保留几位小数，于是 我们不妨用 acos（-1）
来利用电脑计算 排的值 然后 利用 acos（1） 除以每一个小三角行对应的a 这就是可以放 固定半径 r 的圆的最大的数量了。

有些情况需要单独讨论， 因为 sin cos 函数 是有范围的 超过范围的上述理论就是 屁话了…………

同时 double 的比较 需要用到 eps， 因为 有误差（可能小数点后好几十位出现误差）

    
    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <cmath>
    using namespace std;
    int main()
    {
        int n;
        double R, r;
        double eps=1e-10;
        double PI=acos(-1);
        while(cin>>n>>R>>r)
        {
            if(n == 1)
            {
                if(R >= r)
                    puts("YES");
                else
                    puts("NO");
                continue;
            }
            double tmp = asin(r/(R-r));///圆心角的一半
            if(PI/tmp-n > -eps)
                puts("YES");
            else
                puts("NO");
        }
        return 0;
    }
    
    

  
  

