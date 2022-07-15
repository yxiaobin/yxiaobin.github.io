---
title: 注意力CBMA到底在网络中做了什么事
date: 2020-11-23 16:22:11
categories: 深度学习
---
###  注意力CBMA到底在网络中做了什么事

  * #####  CBMA网络架构 

    #####  ![img1](https://img-blog.csdnimg.cn/20200603162817846.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjkwNzQ3Mw==,size_16,color_FFFFFF,t_70)

    *   通道注意力    <!-- more--> 



![img2](https://img-blog.csdnimg.cn/20200603163856177.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjkwNzQ3Mw==,size_16,color_FFFFFF,t_70)

空间注意力：

![im](https://img-blog.csdnimg.cn/20200603164706942.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjkwNzQ3Mw==,size_16,color_FFFFFF,t_70)

  * 分析 

    * 通道注意力： 

      * 1.将特征图进行最大池化和平均池化 

 SENet也使用了通道注意力，
但SENet只采用了平均池化，没有采用最大池化。作者加入了最大池化的原因，在论文中写到是因为在实验中发现加入了最大池化效果更好，或许是因为加入了最大池化获取的信息更丰富。最大池化和平均池化都是global级的，因此相当于一个通道上所有的特征图会压缩成一个像素的特征，n个通道对应n个像素的特征。

      * 2.将池化后的输出经过多层感知器(全连接层) 

作用是学习参数

      * 3.经过一个softmax函数 

目的是获取重要程度

######  为什么起作用：

######
注意力机制实际上就是集中注意到某一个局部，换句话说就是不平等的对待总体的输入，例如，对于一个通道注意力模块来说，对于某特征图输入的所有通道的特征图来说，重视程度是不同的，对于某些通道更重视，权重更大，对于另外某些通道来说就不重视，权重较小，softmax函数的作用就是生成对于各个通道重视程度的概率

    * 空间注意力 
    
      * 首先沿着通道级别最最大池化和平均池化 

沿着通道做，将n个通道HxW的图像压缩为一个单通道的HxW的图像，经过一个1x1的卷积层学习参数，在经过softmax获取HxW上个像素点的重要程度，原理同通道注意力一样。

