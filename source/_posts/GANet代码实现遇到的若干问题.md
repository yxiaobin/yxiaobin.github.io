---
title: GANet代码实现遇到的若干问题
date: 2020-11-19 22:14:18
categories: 深度学习
---
###  GANet代码实现遇到的若干问题

######
开学以来一直在看立体匹配相关方向的论文，为了锻炼一下代码能力，最近几天试图将两个网络进行合并，构建成一个网络测测效果，主要是锻炼一下动手实践能力，遇到了一些问题，现在记录在下面。

  * 运行 ` sh compile.sh ` 编译错误，报错： ` no model libs.GANet.build.lib ` 。编译错误主要因为一下<!-- more -->几个问题： 

    * 注意自己服务器gcc的版本( ` gcc -v ` 查看，需要升级到4.9及以上) 
    * 注意自己的CUDA版本，CUDA版本需9.2及以上，9.0的编译也有问题。 
  * 程序跑在一半过程中卡住，程序不动了。 

    * ` libs.sync_bn ` 模块的同步BN问题，多线程死锁问题，可以换一下别的同步BN模块，再来进行测试是否还会出现此问题。 
  * ` DisparityRegression ` 函数报错非法内存访问 ` RuntimeError: cuda runtime error (77) `

    * 引起错误的是语句 

` disp = Variable(torch.Tensor(np.reshape(np.array(range(self.maxdisp)),[1,
self.maxdisp, 1, 1])).cuda(), requires_grad=False) `

准确的说是 ` .cuda() `
非常奇怪的是，有时候能跑通几次，然后在程序运行过程中抛出这个错误，有的时候直接在第一次求损失就抛出这个错误，我怀疑原因是多卡运算造成的内存非法访问问题，切换为1卡就不会有这个错误了，但是单卡现存负担太大。不同人遇到的原因可能不同，建议查看
` https://discuss.pytorch.org/t/weird-cuda-illegal-memory-access-error/8848/16
`

  * 单卡可跑，但是多卡运行的时候就卡主不动 

    * 注意设置一下 ` batchsize ` 的值,若你指定了3块GPU，但是 ` batchsize=1 ` 就会卡住，应该也设置为3才可。 

