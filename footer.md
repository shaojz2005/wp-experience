# WordPress页脚模板footer.php

footer.php用于调用网站页脚需展示的公共内容，如底部导航菜单、联系方式、版权信息等。

在其它模板里，一般是通过以下函数调用页脚：
```php
<?php get_footer(); ?>
```
其中，get_footer()可以接受一个字符串参数，如果带上了参数，如get_footer('aaa')，则会调用footer-aaa.php模板，可以根据项目不同页面的需要，调用不同的页脚模板。

** 注意 **：
在页脚文件的body标签结束之前，需要调用 wp_footer() 函数，这会自动加载一些wp需要的js脚本文件，对于某些插件来说是必不可少的。

一个典型的footer.php文件如下：

```html
<footer>
    <!-- 底部菜单、版权信息、社交媒体、二维码等 -->
</footer>
<?php wp_footer();//必须在body结束标记前引用wp_footer() ?>
</body>
</html>
```