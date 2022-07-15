---
title: 利用requests库爬取搜狗图片并存入文件夹下
date: 2018-04-17 22:29:42
categories: Python
---
看了一篇帖子， [ https://www.cnblogs.com/dearvee/p/6558571.html
](https://www.cnblogs.com/dearvee/p/6558571.html)
这篇帖子作为一个引导，摸索着完成了第一个爬虫，现在将过程总结如下。

搜狗图片地址为 [ http://pic.sogou.com/ ](http://pic.sogou.com/) ，<!-- more -->利用BeautifulSoup抓取
img 然后打印可以发现 img=“” 都是空的（具体空的详细方法在上面的链接中）

通过F12 检查找到ssh

![](https://img-
blog.csdn.net/20180417222805214?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODA2NDgxMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)  

可以看到 Requests 的 URL ，其中 有几个参数 category tag start len，

![](https://img-
blog.csdn.net/20180417222829197?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODA2NDgxMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)  

实际上 category 指的是 美女 搞笑 壁纸 明星 等分栏

tag指的是下面的 搞笑人物 招牌标题等

start指从第几个开始 len指示一共需要多少个

！！！！！！！！！

这个时候又遇到一个问题，那就是上述的Url里面是一串字母而不是汉字，我们需要解决这个问题

Python中有将汉字转化为Url中字符串的函数为 **urllib.quote()** （不会的同学可以百度）

通过 Preview 可以看出 他们都在一个字段为 all_items 的json里面（代码中 all_items的由来）

![](https://img-
blog.csdn.net/20180417222839454?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODA2NDgxMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)  

在分析其中具体的一个：

![](https://img-
blog.csdn.net/20180417222848708?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODA2NDgxMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)  

每一个都储存在一个 ‘bthumbUrl’里面（代码中 该字段的由来）

理清这些东西就可以写代码了 代码如下

> from bs4 import BeautifulSoup  
>  import requests  
>  import os  
>  import json  
>  import urllib  
>  import random  
>  #爬取图片目标地址
>
> print(“请从以下种类中（搞笑、美女、汽车）中选取一个输入”)  
>  cat = raw_input()  
>  print(“请输入爬取的个数”)  
>  n = raw_input()  
>  print(n)  
>  #%E7%BE%8E%E5%A5%B3  
>  print(‘正在搜索相关的图片’)  
>  url =
> “http://pic.sogou.com/pics/channel/getAllRecomPicByTag.jsp?category=”+
> urllib.quote(cat) + “&tag=%E6%B8%85%E7%BA%AF&start=0&len=”+ str(n)
>
> #利用requests库得到解析网页html  
>  x = requests.get(url, timeout = 30)  
>  x.raise_for_status();  
>  html = x.text
>
> #利用json与热汤库定位解析  
>  soup = BeautifulSoup(html,’html.parser’)  
>  img = json.loads(html)  
>  img = img[‘all_items’]
>
> #存取目标列表的列表名  
>  ulist = []  
>  #将图片url存入列表  
>  for j in img:  
>  ulist.append(j[‘bthumbUrl’])
>
> #存取图片的路径  
>  ear =random.randint(1, 100254)  
>  root = ‘D://pics//’
>
> print(‘————–正在下载图片————————-‘)
>
> #逐个爬取立标里面的url链接  
>  k = 1  
>  for i in ulist:  
>  image_url =ulist[k-1]  
>  image_path = root + str(k)+’.jpg’  
>  try:  
>  r = requests.get(image_url)  
>  r.raise_for_status()  
>  if not os.path.exists(root):  
>  #创建文件夹  
>  os.mkdir(root)  
>  if not os.path.exists(image_path):  
>  r = requests.get(image_url)  
>  with open(image_path, ‘wb’) as file_obj:  
>  file_obj.write(r.content)  
>  print(‘第’+ str(k) +’张图片保留成功’)  
>  except:  
>  print(‘第’+ str(k) +’张图片爬取失败’)  
>  k=k+1
>
> print(‘————–图片下载完成————————-‘)

