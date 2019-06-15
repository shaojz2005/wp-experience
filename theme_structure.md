# WordPress主题模板结构

WordPress的开发主要是在主题模板里进行的。通过主题模板，我们不必更改WordPress的核心文件，就可以自定义网站界面和调用数据逻辑。

## WordPress目录结构

首先，我们来看看WordPress的主目录结构，下面主要列出我们可能用得到的部分。更详细的说明可参考 https://www.cnblogs.com/liuhongfeng/p/5369218.html

> |-wp-admin　　　wp后台程序文件,一般不进行修改
> |-wp-content　　　wp“内容”目录,非常重要,主题、插> 件、上传附件及语言文件都放在这里
> 　||-languages　　　wp语言目录
> 　||-plugins　　　wp插件目录，后台安装的插件都放在> 这里
> 　||-themes　　　wp主题模板目录，一个模板作为一个子目录存放
> 　||-upgrade　　　wp升级文件
> |-wp-includes　　　wp核心文件目录，一般不进行修改
> index.php　　　wp的入口文件，调用核心文件，一般不> 需进行修改
> wp-config.php　　　wp配置文件，可配置wp连接数据库的参数，也可以放入希望全局运行的函数

***

themes是我们放置模板文件的地方，一般一个模板一个目录，wp后台会识别这个目录下的模板，以供用户选择启用哪个模板。

一般来说，我们的wp网站都是定制开发的，而不是通用的博客网站，因此模板都跟具体的后台数据进行关联，不能用于其它网站。如果是多设备适配的网站，可以针对不同的设备（电脑、平板或手机端）设定不同的模板。

## WordPress模板文件结构

- index.php 主模板文件。 所有主题都是必需的。
- style.css 主要样式表。 它在所有主题中都是必需的，并且包含主题的信息标题。
- comments.php 评论模板。
- front-page.php 首页模板始终用作站点首页（如果存在），无论管理员>设置>阅读上的设置如何。
- home.php 默认情况下，主页模板是首页模板。 如果您没有将WordPress设置为使用静态首页，则此模板用于显示最新的帖子。
- header.php 标题模板文件通常包含您的站点的文档类型，元信息，样式表和脚本的链接以及其他数据。
- singular.php 单独的模板用于没有找到single.php的帖子，或者当没有找到page.php的页面时。 如果没有找到singular.php，则使用index.php。
- single.php 当访问者请求单个帖子时，使用单个帖子模板。
- single-{post-type}.php 访问者从自定义帖子类型请求单个帖子时使用的单个帖子模板。
- archive-{post-type}.php 当访问者请求自定义帖子类型归档时，将使用归档文件类型模板。
- page.php 当访问者请求单独的页面（内置模板）时，将使用页面模板。
- page-{slug}.php 访问者请求特定页面时使用页面插件模板，例如使用“about”slug（page-about.php）的页面插件模板。
- category.php 当访问者按类别请求帖子时，将使用类别模板。
- tag.php 当访问者通过标签请求帖子时，使用标记模板。
- taxonomy.php 当访问者在自定义分类法中请求术语时，将使用分类术语模板。
- author.php 访问者加载作者页面时，将使用作者页面模板。
- date.php 日期/时间模板在通过日期或时间请求帖子时使用。 
- archive.php 当访问者按类别，作者或日期请求帖子时，使用归档模板。 注意：如果存在类似于category.php，author.php和date.php的更多特定模板，则此模板将被覆盖。
- search.php 搜索结果模板用于显示访问者的搜索结果。
- attachment.php 当查看单个附件（如图像，pdf或其他媒体文件）时，将使用附件模板。
- image.php 图像附件模板是attachment.php的更具体的版本，在查看单个图像附件时使用。 如果不存在，WordPress将使用attachment.php。
- 404.php 当WordPress找不到与访问者请求相匹配的帖子，页面或其他内容时，将使用404模板。

这里有些模板是为博客网站而设的，如date.php、archive.php、tag.php，我们在开发定制网站时一般不用。

对于附件页面模板文件，如attachment.php、image.php，我们很少会单独显示附件文件，都是包含在图文混排的文章页面里的，因此也很少使用。

front-page.php、home.php用于首页展示，但由于定制网站的首页一般需要展示一些自定义字段内容，因此需要使用页面来定制和调用字段，一般也不使用这两个模板文件了。

## WordPress的模板层级机制

WordPress的前台展示页面有很多种，主要包括首页、列表页和详情页等。当我们请求一个WordPress内容时，WordPress会依据一定的层级顺序寻找模板文件，找到匹配的就优先使用展示。这个层级顺序十分重要，理解这个机制有助于我们使用合理的模板文件来调用我们的数据。

对于WordPress的层级顺序，官方有一个详细的结构图进行说明：

![wordpress模板层级](img\Screenshot-2019-01-23-00.20.04.png)

详细说明可参考：https://developer.wordpress.org/themes/basics/template-hierarchy/