# WordPress文件结构

我们来看看wp的主目录结构，下面主要列出我们可能用得到的部分。更详细的说明可参考 https://www.cnblogs.com/liuhongfeng/p/5369218.html

> |-wp-admin　　　wp后台程序文件,一般不进行修改  
> |-wp-content　　　wp“内容”目录,非常重要,主题、插件、上传附件及语言文件都放在这里  
> 　||-languages　　　wp语言目录  
> 　||-plugins　　　wp插件目录，后台安装的插件都放在这里  
> 　||-themes　　　wp主题模板目录，一个模板作为一个子目录存放  
> 　||-upgrade　　　wp升级文件  
> 　||-uploads　　　wp附件文件  
> |-wp-includes　　　wp核心文件目录，一般不进行修改  
> index.php　　　wp的入口文件，调用核心文件，一般不需进行修改  
> wp-config.php　　　wp配置文件，可配置wp连接数据库的参数，也可以放入希望全局运行的函数  

themes目录是我们放置模板文件的地方，一般一个模板一个目录，wp后台会识别这个目录下的模板，以供用户选择启用哪个模板。

plugins目录用于存放wp插件，我们可以下载插件解压到这个目录，或者从后台直接安装插件。

uploads目录放置用户上传的媒体文件，包括图像、PDF以及其它格式的内容。