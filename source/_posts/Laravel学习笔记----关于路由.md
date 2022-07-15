---
title: Laravel学习笔记----关于路由
date: 2018-03-18 15:09:50
categories: Laravel
---
一：

定义路由有两种方式：

1\.

    
    
    Route::get('/', function () {
        return view('welcome');
    });

Route 就是路由的关键字了； :: 表是是路由的静态方法 get post put 等是html中的方法

‘/’表是url里面的路径了 function就是功能函数了

2\.

 <!-- more -->   
    
    Route::get('/posts','\App\Http\Controllers\PostControllers@index');

第二种方法是我们常用的方法，因为这样书写使得web.php的路由层显得整齐，

基本格式为：

    
    
    Route::get('/' , '控制器@函数名')

二：路由的各种方法

    
    
    Route::get('/' , '控制器@函数名')
    // GET
    Route::get('/posts','\App\Http\Controllers\PostControllers@index');
    //POST
    Route::post('/posts','\App\Http\Controllers\PostControllers@index');
    //PUT
    Route::put('/posts','\App\Http\Controllers\PostControllers@index');
    // 支持各种格式
    Route::any('/posts','\App\Http\Controllers\PostControllers@index');
    //支持指定格式
    Route::match(['get', 'post'], '/posts', '\App\Http\Controllers\PostControllers@index');
    //路由参数
    Route::get('/posts/{id}','\App\Http\Controllers\PostControllers@index');

那么问题来了，什么是路由参数？

emmm，看这篇文章的 url链接出 为 http://mp.csdn.net/postedit/79600715

假设写一个这个的get方法：

Route::get('/postedit/{id}', '控制器@函数名')

如你所见 79600715 对应的就是参数 id了

三：路由分组

假定有一下三个路由：

（注意这三个路由的 函数名 应该是不同的三个，当时为了记录方便，没有修改）

    
    
    Route::get('/posts','\App\Http\Controllers\PostControllers@index');
    Route::get('/posts/{id}','\App\Http\Controllers\PostControllers@index');
    Route::get('/posts/delete','\App\Http\Controllers\PostControllers@index');

他们的 URL 访问 都用同一层的 posts

那么这三个路由就可以归并为一个组，写法如下：

    
    
    Route::group(['prefix' => 'posts'],function (){
        Route::get('/', '\App\Http\Controllers\PostControllers@index');
        Route::get('/{id}', '\App\Http\Controllers\PostControllers@index');
        Route::get('/delete', '\App\Http\Controllers\PostControllers@index');
    })

  

  

  

  

  

