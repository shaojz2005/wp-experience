# WordPress模板默认样式文件

WordPress模板中有一些默认命名的样式文件，这些文件用于标记识别模板，或用于为指定的界面定制样式。

## style.css
这是wp模板的主样式文件，最重要的在于文件头部包含一段注释，这段注释记录了模板的一些基本信息，直接作为后台识别和选择模板的依据。如果没有style.css文件或者没有包含正确的注释，则这个模板不能被后台识别和启用。

style.css的注释格式为：
```css
/*
Theme Name: t4t
Theme URI: 
Description: t4t theme
Author: Aeven
Version: 1.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: t4t
*/
```
其中Theme Name最为重要，同一个wp站点中不能有相同Theme Name的两个模板，其它信息则没什么作用。

style.css必须放在模板根目录下。

由于前端现在都流行工程化，样式文件也会根据用途分开不同的文件，因此style.css显得不太够用。我通常的做法是只在style.css里写模板声明注释，而不写css规则。

## editor-style.css
顾名思义，这是定义编辑器样式，会在后台加载富文本编辑器时加载样式。为了保持前后台的显示效果一致，可以把文章详情的css规则粘贴到这里。

editor-style.css必须放在模板根目录下。

## admin-style.css
顾名思义，这是访问后台加载的样式，理论上来说你可以使用这个样式来重定义后台的界面风格。但由于后台是给管理用户使用的，界面不必定制得太精美。所以我们使用这个样式文件，更多是为了隐藏后台一些内容，或者微调它们的展示方式。

admin-style.css必须放在模板根目录下。

---

如上所述，这三个wp默认的样式文件，实际上用得不多。但在有特殊需求时，有技巧地使用这些样式文件，可以达到意外的效果。