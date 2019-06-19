# WordPress页头header.php

header.php用于调用网页头需展示的内容，包括HTML的head声明内容以及公共的页头内容，如logo、顶部导航菜单等。

在其它模板里，一般是通过以下函数调用页头：
```php
<?php get_header(); ?>
```
其中，get_header()可以接受一个字符串参数，如果带上了参数，如get_header('aaa')，则会调用header-aaa.php模板，可以根据项目不同页面的需要，调用不同的页头模板。

**注意**：
在页头文件的head标签结束之前，需要调用 wp_head() 函数，这会自动加载一些wp需要的css和js脚本文件，对于wp正常运行是必不可少的。

一个典型的header.php文件如下：

```html
<!doctype html>
<html>
<head>
    <!-- 头部meta -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <meta http-equiv="X-UA-Compatible" content="IE=edge, chrome=1">
    <meta name="renderer" content="webkit">
    <title><?php
    //灵活调用变量作为网页标题
    global $page, $paged;
    wp_title('|', true, 'right');
    bloginfo('name');
    $site_description = get_bloginfo('description', 'display');
    if ($site_description && ( is_home() || is_front_page() ))
        echo " | $site_description";
    if ($paged >= 2 || $page >= 2)
        echo ' | ' . sprintf(__('Page %s', 'twentyten'), max($paged, $page));
    ?></title>
    <!-- 这里可以调用自己定义需要加载的模板css和js文件，注意最好放在wp_head()之前 -->
    <?php wp_head();//必须在head结束标记前引用wp_head() ?>
</head>
<body>
<header>
    <!-- logo、头部导航、多语言切换等 -->      
</header>
```