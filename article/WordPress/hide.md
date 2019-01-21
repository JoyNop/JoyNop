最近在搞一个软件资源分享的网站，思考了很久选择什么样的框架，最后还是选择了经典WordPress

选择他的原因无非是因为，维护方便，毕竟PHP是世界上最好的语言

相信很多同学在一些博客当中看到有些内容需要登录后、回复后或输入密码后才能看到，是不是觉得很有意思，可以相对的增加与访客的互动，特别是加密后输入密码可见可以上部分内容只针对特点人群开放。在此文章中蜗牛将为大家分享如何通过插件或代码来隐藏WordPress文章部分内容，让用户登录或输入密码后才能看见

## 方法一：插件

首先推荐一款小巧的插件—Login to view all，来实现使隐藏WordPress文章部分内容，让用户登录后可见。用插件的还出是简单便捷，只需下载插件并上传安装好启用即可。

1. 百度网盘下载Login to view all：https://pan.baidu.com/s/1qYxDMNy 密码: 6xtk

2. WordPress官方下载：https://wordpress.org/plugins/login-to-view-all/

关于插件的使用及效果，就不做演示了，大家自己体验。

插件版优缺点：

使用插件版后，如果不想使用插件了，我们屏蔽插件后，原先文章内隐藏的内容会直接消失掉。这个缺点很致命，要用此插件就要决定长期使用下去。优点是与CDN加速兼容性较好，不会存在登录不显示内容的现象。

## 方法二：代码

个人更倾向于使用代码，这里为大家分享三种方法，最后一种是实现输入密码后才能显示。与插件版相比，代码版优缺点也是各半，大家自己斟酌选择。

代码版优缺点：优点是与插件版相比，我们不想使用此功能时，取消相应代码，原先隐藏的内容会正常显示。缺点是与CDN加速兼容较差，会被缓存，如果你的站点开启了CDN加速，会出现登录也无法显示内容的情况。

### 简单版
在主题的functions.php文件添加以下代码：

```php
//部分内容登录可见 
add_shortcode('hide','loginvisible');
function loginvisible($atts,$content=null){
	if(is_user_logged_in() && !is_null($content) && !is_feed())
	return $content;
	return '';
}
```

如何实现？在编辑文章是使用短码包围要隐藏的内容，如：（把下面中文括号改为英文括号【】→[]）

>`[hide]`登陆才可以看到的内容`[/hide]`

是不是很简单，这里无作为暂时先分享个文章登录可见的的方法，下次会分享关于wordpress回复可见的方法！

### 美化版

在主题function.php文件里加入以下代码。其中可用于直接将`href=”#respond”`后的`“#respond”`替换为自己站点的登录地址，以方便用户快速登录。

```php
//部分内容登录可见  
function login_to_read($atts, $content=null) {
extract(shortcode_atts(array("notice" => '
<span style="color: red;">温馨提示：</span>此处内容需要<a title="登录后可见" href="#respond">登录</a>后才能查看！
'), $atts));
if ( is_user_logged_in() && !is_null( $content ) && !is_feed() )
 return $content;
 return $notice;
}
add_shortcode('vip', 'login_to_read');
 ```

如何实现？在编辑文章是使用短码包围要隐藏的内容，下面列举的是两种方式，我们任选一种即可。

>`[vip]`我是被隐藏的内容，样式一（默认样式）`[/vip]`

>`[vip] notice="登录后才显示哟"]`我是被隐藏的内容，样式二（自定义回复信息）`[/vip]`


### 输入密码显示
首先在主题`functions.php`文件中添加下面代码。

```php
//部分内容输入密码可见 
function e_secret($atts, $content=null){
  extract(shortcode_atts(array('key'=>null), $atts));
  if(isset($_POST['e_secret_key']) && $_POST['e_secret_key']==$key){
    return '
    <div class="e-secret">'.$content.'</div>';
    }else{
      return '
      <form class="e-secret" action="'.get_permalink().'" method="post" name="e-secret"><label>输入密码查看加密内容：</label><input type="password" name="e_secret_key" class="euc-y-i" maxlength="50"><input type="submit" class="euc-y-s" value="确定">
      <div class="euc-clear"></div></form>';
      }
  }
add_shortcode('secret','e_secret');

```

第二步到在自己主题`main.css`或者`style.css`样式文件里添加下面代码。

```css
/*e-secret*/
.e-secret {
 margin: 20px 0;
 padding: 20px;
 background: #f8f8f8;
}
.e-secret input.euc-y-i[type="password"] {
 float: left;
 background: #fff;
 width: 100%;
 line-height: 36px;
 margin-top: 5px;
 border-radius: 3px;
}
.e-secret input.euc-y-s[type="submit"] {
 float: right;
 margin-top: -47px;
 width: 30%;
 margin-right: 1px;
 border-radius: 0 3px 3px 0;
}
input.euc-y-s[type="submit"]{background-color:#3498db;color:#fff;font-size:21px;box-shadow:none;-webkit-transition: .4s;-moz-transition: .4s;-o-transition: .4s;transition:.4s;-webkit-backface-visibility:hidden;position:relative;cursor:pointer;padding: 13px 20px;text-align: center;border-radius: 50px;-webkit-box-shadow: none; -moz-box-shadow: none; box-shadow: none;border: 0;height: auto;outline: medium;line-height: 20px;margin: 0;}
input.euc-y-s[type="submit"]:hover{background-color:#5dade2;}
input.euc-y-i[type="text"],input.euc-y-i[type="password"]{border:1px solid #F2EFEF;color:#777;display:block;background: #FCFCFC;font-size:18px;transition:all .5s ease 0;outline:0;box-sizing:border-box;-webkit-border-radius:25px;-moz-border-radius:25px;border-radius:25px;padding:5px 16px; margin: 0;height: auto;line-height: 30px;}
input.euc-y-i[type="text"]:hover,input.euc-y-i[type="password"]:hover{border:1px solid #56b4ef;box-shadow:0 0 4px #56b4ef;}

```

如何实现？在编辑文章是使用短码包围要隐藏的内容，如下即可。

>`[secret key="密码"]`加密内容`[/secret]`