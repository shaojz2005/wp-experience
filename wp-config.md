#wp-config.php的常用配置参数

wp-config.php在wp根目录下，是wp的核心配置文件，包括数据库连接参数都在这个文件里配置，十分重要。下面列出几个重要的配置内容。

```php
/** WordPress数据库的名称 */
define('DB_NAME', '******');
/** MySQL数据库用户名 */
define('DB_USER', '******');
/** MySQL数据库密码 */
define('DB_PASSWORD', '******');
/** MySQL主机 */
define('DB_HOST', 'localhost');
/**
 * WordPress数据表前缀。
 *
 * 如果您有在同一数据库内安装多个WordPress的需求，请为每个WordPress设置
 * 不同的数据表前缀。前缀名只能为数字、字母加下划线。
 */
$table_prefix  = 'wp_';
```
这是wp配置数据库连接的四大参数，一般在迁移网站到新的服务器时，需要修改这些内容。

```php
/**#@+
 * 身份认证密钥与盐。
 *
 * 修改为任意独一无二的字串！
 * 或者直接访问{@link https://api.wordpress.org/secret-key/1.1/salt/
 * WordPress.org密钥生成服务}
 * 任何修改都会导致所有cookies失效，所有用户将必须重新登录。
 *
 * @since 2.6.0
 */
define('AUTH_KEY',         'Kl7t+3jb`>Y(55p+8S[o35+?DFr?GPq5]AJoM]`!vasxcvF2*O+k1}.>}`d{RxEe');
define('SECURE_AUTH_KEY',  'c/Pb_w3e(544@%4T7@`8Go[UwSAMkP+uoqw234YzHW6eVBTG4(7kcmU#aqeQs_k.');
define('LOGGED_IN_KEY',    'm8=!8/#=#Fe.w366pkjQY5<PZ!cia:;&J*x6*r&(on<f,T**************$EcN');
define('NONCE_KEY',        '/7|XfMkSQ&6w>v%c77grn_](H$/kAw>q}x/:e~PX>yUh+``)t8**********gA}X');
define('AUTH_SALT',        '%Z@@Jsbnhyu_<ueh*d88-ADq`Q9PWu1*EPjPoYyZU***************(1eY2)a`');
define('SECURE_AUTH_SALT', 'XJ1Rq<+C|&M&^hgfho=E99!NeB,]y~ArwcTZn>e@D:@**************SB&D?Z/');
define('LOGGED_IN_SALT',   'L)O|ilkjq@E%%1RLR:oo)H.6jl:;f#M&k+BwP-*****12S-C#%)fz?/YoQ3%mX*9');
define('NONCE_SALT',       'x]P&~> ;2Vj{&s^$Z}a***********************ir?XBP!OEh-l8eHvlt)sSs');
```
这是wp用于进行身份认证传输的加密配置，出于安全，最好每个网站都采用不同的配置内容。如上注释所提示，可以访问https://api.wordpress.org/secret-key/1.1/salt/ 来生成随机的密钥。

```php
define('WP_DEBUG', false);
```
这是wp的调试模式开关，当遇到问题需要输出错误调试时，设置为true，但正式上线的网站应该设置为false。


此外还有一些额外的配置，可以让wp运行得更好，可以加入到这个配置文件中。

```php
define('WP_HOME','http://'.$_SERVER['HTTP_HOST']);
define('WP_SITEURL','http://'.$_SERVER['HTTP_HOST']);
```
在迁移网站时，有时需要更换域名。wp的域名配置是写在数据库的配置表里面的，更换域名之后会出现一些重定向的问题，只要在wp-config.php里加上这2个配置，就可以灵活适配新的域名了。这也是实现多域名指向同一网站的方法。

```php
define('WP_POST_REVISIONS', false);//禁用历史修订版本
define('AUTOSAVE_INTERVAL', 86400);//设置自动保存时间设置为一天
```
由于wp是博客出身，有一些机制是为博客而生的，例如历史修订版本和自动保存功能，这些功能会带来很多不必要的数据库记录，可以通过这两行配置进行禁用。
