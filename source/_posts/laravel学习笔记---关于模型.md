---
title: laravel学习笔记---关于模型
date: 2018-03-21 19:25:40
categories: Laravel
---
1\.

模型层一般放在 \app\http 下

创建模型语句 php artisan make:model ModelName

一般情况下，建立的模型与其表是相对应的，如果想与其他表对应，需要在模型函数里面声明

    
    
    class Post extends Model
    {
        //
        protected  $table = '目标表的名<!-- more -->字' ;
    }

一般情况下使用都是一一对应，这样方便。

2\.

控制器中要引用相关的模板

例如：use App\Post;

举个例子，将数据表中的文章按照时间排序获得可用下面的语句

    
    
    public  function  index(){
       $post = Post::orderBy('created_at','desc')->get();
        return view("post/index", _compact_ ('post'));
       // return view("post/index", ['post' => $post]);
    }

  

  

  

