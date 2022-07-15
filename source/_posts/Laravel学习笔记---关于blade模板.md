---
title: Laravel学习笔记---关于blade模板
date: 2018-03-19 21:15:38
categories: Laravel
---
一： 模板语法

1\. {  {}}---传递参数

控制器中 return view 的第二个参数是传递一个数组

比如：

    
    
    public  function  show(){
        return view("post/show",['tittle'=>'this is tittle']);
    }

那在前端文件 show.blade.php中的参数<!-- more -->传递语句为：

    
    
    < **h2** class= **"blog-post-title"** >{{ $tittle }}</ **h2** >

2.@if()开始 用@endif()结尾的 条件语句

比如：

    
    
    public  function  show(){
        return view("post/show",['tittle'=>'this is tittle', 'isShow'=>false]);
    }

前端显示语句为：

    
    
     @if($isShow == true)
    < **a** style= **"** _margin_ : **auto** **"** href= **"/posts/62/edit"** >
         < **span** class= **"glyphicon glyphicon-pencil"** aria-hidden= **"true"** ></ **span** >
     </ **a** >
     @endif

上式子可以看出，因为 isShow 的值是false 所以此a标签不会显示

3.@foreach() 开头@endforeach 结束的 循环语句

百度用法如下：

    
    
    foreach 可以遍历数组与对象，它会把当前单元的键名也会在每次循环中被赋给变量 $key，值赋给变量$val，例如  
     $row=array('one'=>1,'two'=>2);  
    foreach($row as $key=>$val){  
        echo $key.'--'.$val;  
      
    }  
    [第一次](https://www.baidu.com/s?wd=%E7%AC%AC%E4%B8%80%E6%AC%A1&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y4uAn1uH6LnWbvuymdrAfz0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPHTYnWfvPjn3)遍历的$key是one，$val是1；  
    第二次遍历的$key是two，$val是2；

举例如下：

    
    
    public  function  index(){
        $post = [
            ['tittle' => 'this is tittle1'],
            ['tittle' => 'this is tittle2'],
            ['tittle' => 'this is tittle3']
        ];
        return view("post/index", ['post' => $post]);
    }

前端显示如下：

    
    
    @foreach($post as $key)
    < **div** class= **"blog-post"** >
        < **h2** class= **"blog-post-title"** >< **a** href= **"/posts/62"** >{{$key['tittle']}}</ **a** ></ **h2** >

！！！！！结尾还有  _@endforeach_

二 参数传递 laravel 框架自带的参数传递方法 compact

    
    
    public  function  index(){
        $post = [
            ['tittle' => 'this is tittle1'],
            ['tittle' => 'this is tittle2'],
            ['tittle' => 'this is tittle3']
        ];
        $pp = ['key' => 'value'];
        return view("post/index", _compact_ ('post', 'pp'));
       // return view("post/index", ['post' => $post]);
    }

  

相比与上一个传递数组更加的简便而已

三：继承模型---制作顶部尾部侧边栏框架

语法知识点：

1.@yield()

2.@extends()

3.section() @endsection

4.@include（）

@yiled('content')

在模板中合适的位置 填充次语句，表示内容

    
    
    < **div** class= **"row"** >
        @yield('content')

在引用模板的语句中利用语句填充内容

    
    
    @extends('layout.main' )
    @section('content')
    
    
    @endsection

@extends（）表是引用模板main

@section（‘content’）与 语句 @endsection 之间填充content内容

将main.blade.php 分层， 可以分成 nav footer sidebar 三块

将一块分出去 另一块用 @include（"layout.nav"）就可以引用使用了

    
    
    @include("layout.header")
    < **div** class= **"container"** >
    
        < **div** class= **"blog-header"** >
        </ **div** >
        < **div** class= **"row"** >
            @yield('content')
            @include("layout.sidebar")
        </ **div** >    </ **div** ><!-- /.row -->
    </ **div** ><!-- /.container -->
    @include("layout.footer")

举个例子：footer.blade.php 中的内容为

    
    
    < **footer** class= **"blog-footer"** >
        < **p** >Blog template built for < **a** href= **"http://getbootstrap.com"** >Bootstrap</ **a** > by < **a** href= **"https://twitter.com/mdo"** >@mdo</ **a** >.</ **p** >
        < **p** >
            < **a** href= **"#"** >Back to top</ **a** >
        </ **p** >
    </ **footer** >

  

  

  

  

