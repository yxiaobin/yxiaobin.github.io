---
title: A water problem--------大数取模
date: 2017-08-15 10:36:00
categories: 数据结构
---
  
Two planets named Haha and Xixi in the universe and they were created with the
universe beginning.  
  
There is 73 days in Xixi a year and 137 days in Haha a year.  
  
Now you know the days N aft<!-- more -->er Big Bang, you need to answer whether it is the
first day in a year about the two planets.  
  
  
Input  
There are several test cases(about 5 huge test cases).  
  
For each test, we have a line with an only integer N(0≤N), the length of N is
up to 10000000.  
  
  
Output  
For the i-th test case, output Case #i: , then output "YES" or "NO" for the
answer.  
  
  
Sample Input  
  
10001  
0  
333  
  
  
  
Sample Output  
  
Case #1: YES  
Case #2: YES  

Case #3: NO

  

知识点整理：

(a+b)%n=(a%n+b%n)%n

  

(a-b)%n=(a%n-b%n+n)%n

  

为什么要加n，由于a%n可能小于b%n,所以加n保证为正整数

  

a*b%n=(a%n*b%n)%n

  

这些事大整数取模的基础

  

int mod(char str[],int num)

{

intnumber[100];

for(inti=0;i<strlen(str);i++)

number[i]=str[i]-'0';

intremainder=0;

for(inti=0;i<strlen(str);i++)

{

remainder=((longlong)remainder*10+number[i])%num;

}

returnremainder;

}

  

之所以强制转换为long long ，是为了防止乘法过程中溢出

  

幂取模

  

int pow_mod(int a,int n,int m)

{

if(n==1) return a;

else

{

int x=pow_mod(int a,intn/2,int m)

long long x=(longlong)x*x%m;

if(n%2==1) x=(longlong)x*a%m;

return (int)x;

}

}

  

