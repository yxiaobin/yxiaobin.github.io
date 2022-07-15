---
title: Laravel学习笔记---项目驱动学习
date: 2018-03-25 17:56:24
categories: Laravel
---
1\. 在前端页面中可以通过 @php @endphp中套用PHP语句

2\.

    
    
    {!!str_limit($key->content,100,'....')  !!}

str_limit() 函数来限制显示的字数最大为100个，超过的用....来代替

3.php自动去除html标签函数

strip_tags（）可以把网页标签  

4.获取制定个数的数组对象
<!-- more -->
    
    
    $hotblogs = $member->blogs()->orderBy('num','desc')->get()->take(3);

这样就可以获取热门博客的前三个

5.自动分页----  paginate

后台分页方法

    
    
    $projects = Member::find( _$id_ )->projects()->orderBy('start_time', 'desc')->paginate(2);

后台分页前端显示方法

    
    
    < **div** class= **"pagination-container margin-top-30"** >
        < **nav** class= **"pagination"** >
            < **ul** >
                {{$projects->links()}}
            </ **ul** >
        </ **nav** >
    </ **div** >

  

这样他会自动显示出 换页代码的

