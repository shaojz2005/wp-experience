# 文章循环的调用方法

文章循环是wp的最核心调用方式。一般我们做cms时，最常用的需求就是调用一个列表或者一篇文章的详情，wp已经在模板文件里集成了一系列的方法来进行调用。另外我们也可以使用特定的函数来按特定的条件调用文章。

## 模板里默认调用文章循环

一个模板文件，根据它的命名，wp已经默认进行了相关的文章调用，并且赋值给全局变量$posts。但是我们并不需要去访问$posts，wp已经给我们配备了一些函数用于循环调用和输出文章的标题、内容等字段。

例如，对于archive-{post-type}.php，这是展示一个自定义文章类型的列表模板。一般我们会通过以下代码进行调用：

```html
<div class="list">
    <?php while(have_posts()): the_post(); ?>
    <a href="<?php the_permalink() ?>" target="_blank" class="item-box">
        <div class="img-box">
            <?php the_post_thumbnail('information'); ?>
        </div>
        <div class="right-content">
            <h3><?php the_title() ?></h3>
            <div class="minor-desc">
                <span class="date no-margin"><?php echo get_the_date() ?></span>
            </div>
            <div class="desc"><?php the_excerpt() ?></div>
        </div>
    </a>
    <?php endwhile; ?>
</div>
```

这里有几个关键点需要明确以下：

1. **have_posts()**：只能用于循环，用于判断循环是否到了最后一个元素，如果还没有就继续运行。
2. **the_post()**：用于循环内，取出一条最新的文章。这两个函数是wp自带的，也是实现文章内容调用的前提。通过while循环来遍历模板的文章数组，通过have_posts()判断是否已经执行到了文章数组中的最后一篇文章，如果还没有，就可以调用the_post()来取出一篇文章，同时把文章指针+1，指向下一篇文章，以便执行下一次循环。

3. **the_title()**：wp自带文章标题调用函数，只能用在文章循环。the_title()读取文章的标题字段，并输出内容展示出来。另外还有get_the_title()，不进行自动输出，因此可以有更多的灵活性来构造特定样式。

4. **the_content()**： wp自带函数，用于获取文章的详情内容，一般输出的是带HTML格式的内容。另外还有get_the_content()用于返回文章详细内容。

5. **the_permalink()**：用于获取当前文章的链接，由于链接可以采用多种内容架构，因此不能写死链接内容，需要通过the_permalink()或者get_permalink()来返回获得。

6. **the_post_thumbnail()**：用于获取文章的封面图，输出为完整的img标签。the_post_thumbnail()可以接受一个参数，作为缩略图的缩放裁减尺寸依据。同样的还有get_post_thumbnail(),用于返回img标签代码。

7. **the_excerpt()**：用于列表页输出wp自带摘要，在文章内容较长时可以使用。

8. **the_date()**：用于输出文章的发布日期，一般用于展示新闻动态的网站栏目。

**特别说明**：