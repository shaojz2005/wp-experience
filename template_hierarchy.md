# WordPress的模板层级机制

wp的前台展示页面有很多种，主要包括首页、列表页和详情页等。当我们请求一个内容时，wp会依据一定的层级顺序寻找模板文件，找到匹配的就优先使用展示。这个层级顺序十分重要，理解这个机制有助于我们使用合理的模板文件来调用我们的数据。

对于WordPress的层级顺序，官方有一个详细的结构图进行说明：

![wordpress模板层级](./img/Screenshot-2019-01-23-00.20.04.png)

一般来说，wp会根据请求的网址字符串来确定使用哪一类的模板来展示内容。在这一类模板中，通常包含有具体针对某一内容的具体模板以及通用的模板。wp会优先使用具体模板，如没有具体模板再往上查找通用模板。因此，我们即可以为某些特殊内容定制具体模板，又可以使用通用模板来展示普适性内容，从而达到灵活展示不同内容的目的。

## 首页

wp的首页机制有点混乱，有些设定是为博客考虑的，现在已经很少用了。首页的调用顺序为：

1. front-page.php
2. home.php
3. page.php
4. index.php

不过，为了定制首页需要的自定义字段（例如：只在首页展示的轮播图），我们一般会设定一个首页模板page-home.php，并建立一个使用这个模板的页面，并在后台设置中指定这个页面为首页。

## 文章详情页

文章详情页包含wp默认的文章类型及自定义文章类型，按以下顺序调用：

1. single-{post-type}-{slug}.php
2. single-{post-type}.php
3. single.php
4. singular.php
5. index.php

## 文章列表页

文章列表页用于展示wp默认的文章类型及自定义文章类型的列表。

1. archive-{post_type}.php
2. archive.php
3. index.php

## 默认文章类别列表页

默认的文章类型有一个关联的文章类别，称为category，是wp自带的。

1. category-{slug}.php
2. category-{id}.php
3. category.php
4. archive.php
5. index.php

## 自定义文章类别列表页

自定义文章类别称为taxonomy，一般是跟自定义文章类型关联的。

1. taxonomy-{taxonomy}-{term}.php
2. taxonomy-{taxonomy}.php
3. taxonomy.php
4. archive.php
5. index.php

## 页面

页面是wp自带的一种内容类型，它没有归档列表页，每个页面都是独立存在的，但具有父子层级关系。

页面有个特别的属性，就是可以指定页面模板，且优先级最高。

1. page-{template-name}.php
2. page-{slug}.php
3. page-{id}.php
4. page.php
5. singular.php
6. index.php

其它的日期、作者等归档页，很少在非博客类型的网站中使用，不再进行介绍。

