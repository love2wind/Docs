# 宝塔面板安装Chevereto图床程序及其常见问题

## 关于Chevereto

Chevereto是一个可以帮助你建立自己的图像分享网站（图床）的应用程序，我们的目标是可以让世界上的任何一个人都可以建立自己的图像共享平台。我们坚定不移的为那些想要可定制的白标图像共享服务的人建立一个真正的替代品。

> 白标：white-label 直译为白标，引申为不注重品牌宣传的产品。Whitelabel致力于研发具有新功能、外形时尚、操作简单的产品，消费者可以尽情享受高科技带来的完美体验。whitelabel不做品牌宣传，我们提倡产品价值的回归，让消费者购买的是产品真正的价值，剔除广告费等一切隐形费用，享受超高性价比。良好的品质和口碑是我们最好的宣传。(摘自百度百科)

![](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/44d63409c7bbae63049ca3885965120b.webp)

官方网站：https://chevereto.com/

官方文档：https://chevereto.com/docs

中文文档：https://ch.cndrew.cn/

DEMO：https://imgbed.top

Chevereto有两个版本，一个付费版，一个免费版。一般情况下个人用户使用免费版就足够了，当然如果是土豪请随意。

购买付费版：https://chevereto.com/pricing

免费版项目地址：https://github.com/chevereto/Chevereto-Free

!> 免费版将于2021.12.31停止更新（[点此查看](https://chevereto.com/community/threads/goodbye-chevereto-free.13510/)），不过现在的功能基本上已经很完善了，完全可以正常运营。当然如果遇上搞活动可以撸一个服务费版，还是比较值得的。

### 系统需求

- Apache or **Nginx （推荐使用的服务器Nginx）
- 5.6版本的PHP（推荐使用7.4版本）和标准库
- MySQL 8 / MariaDB 10

!> chevereto官方要求MySQL版本是8.0，但是我在使用时5.7也是可以的，据说不能低于5.6，本人没有 测试，大家有兴趣可以测试一下。另外由于最新版本支持webp，所以PHP最低版本也要是7.4了

## 宝塔面板安装

Chevereto支持多种安装方式，我们在[中文文档](https://ch.cndrew.cn/cn/Setup/Install/)里可以看到可以通过`installer.php`安装文件直接安装，还可以通过**docker**安装，还有ZIP文件、cPanel、Softaculous/Fantastico等多种方法，这里我们主要介绍下大家喜闻乐见的宝塔面板下的安装方法。

### 安装前的环境准备

1. 安装宝塔面板（宝塔服务器面板，一键全能部署及管理，送你3188元礼包，点我领取https://www.bt.cn/?invite_code=MV9wamtyb2E=）
2. 在宝塔面板里部署好环境，Nginx+PHP+Mysql并成功启动（付费版需要安装fileinfo、exif两个扩展）
3. 一个域名
4. 在宝塔面板新建一个网站和MySQL数据库
5. 配置好SSL

### 安装步骤

#### 1）下载程序文件

过宝塔面板文件管理器打开新建的网站目录，下载 [Chevereto free](https://github.com/chevereto/Chevereto-Free/archive/refs/tags/1.4.1.zip) 文件，如果你购买了付费版这里就下载上传付费版文件。

#### 2）设置文件权限

Chevereto需要在以下路径中写入并存取（递归权限）：

- `app/content`
- `app/content/languages`
- `app/content/languages/cache`
- `app/content/locks`
- `app/content/system`
- `content`
- `images`

Chevereto使用PHP和Web服务器（Apache，Nginx等）继承其对Chevereto的权限，因此如果Apache无法写入文件夹，那么Chevereto将无法在其上写入。确保Web服务器位于网站文件夹的root文件夹中，以保证Chevereto可以正常工作。

还要仔细检查对temp文件夹的读/写访问权限（Unix/Linux中的`/tmp`和Windows中的`C:/Windows/Temp`）。

#### 3）Nginx伪静态配置

```nginx
# Image not found replacement
location ~* (jpe?g|png|gif) {
        log_not_found off;
        error_page 404 /content/images/system/default/404.gif;
}

# CORS header (avoids font rendering issues)
location ~ \.(ttf|ttc|otf|eot|woff|woff2|font.css|css|js)$ {
        add_header Access-Control-Allow-Origin "*";
}

# Pretty URLs
location / {
        try_files $uri $uri/ /index.php?$query_string;
}
```

#### 4）访问你的站点域名开始安装

![](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/82a623ad37d540cfd029b38d85a4c112.webp)

**app/settings.php 的配置示例**

此文件包含应用程序设置，如数据库凭据和其他设置。此文件可能如下所示：

```php
<?php
$settings['db_host'] = '127.0.0.1';
$settings['db_port'] = 'port';
$settings['db_name'] = 'name';
$settings['db_user'] = 'user';
$settings['db_pass'] = 'password';
$settings['db_table_prefix'] = 'chv_';
$settings['db_driver'] = 'mysql';
$settings['debug_level'] = 1;
```

#### 5）登录进入后台，开始配置网站。

不出意外的话，非常简单就能完成安装，然后即可登录进入后台仪表盘进行配置了。

默认会根据登录地址IP自动判断语言，也有可能默认是英文，那么我们就先要设置成中文。

?> 点击右上角头像 -- Dashboard -- settings -- Lanuages -- Default language -- 简体中文

这样我们就可以根据提示，对图床进行配置了。

## 常见问题汇总

#### 1）首页添加网站图片数量

修改 `app/themes/Peafowl/views/index.php` 大约在32行的适当位置添加下面代码：

```php
<p>目前本站已安全托管 <?php $stats = CHV\Stat::getTotals(); echo $stats['images'] > 999999 ? $stats['images'] : number_format($stats['images']); ?> 张图片</p>
```

#### 2）添加备案信息

修改 `app/themes/Peafowl/views/index.php`  找到下述代码：

```php
<div class="footer"><?php _se('Powered by'); ?> <a href="https://chevereto.com" rel="generator">Chevereto</a></div>
```

替换成类似如下代码即可。

```php
<div class="footer"><a href="http://www.beian.miit.gov.cn" target="_blank">沪ICP备12345678号</a></div>
```

#### 3）通过api上传图片到指定用户、指定相册

API V1没有办法上传与给定用户相关联的图像，但是你可以覆盖默认的API，将默认的`app/routes/route.api.php`的文件复制到`app/routes/overrides/route.api.php`文件夹。

**105行下列内容**

```
CHV\Image::uploadToWebsite($source);
```

**改成这个**(将 `juanito` 更换成目标用户名或用户id)

```php
// 这将会为juanito用户上传图片
$uploaded_id = CHV\Image::uploadToWebsite($source, 'juanito');
```

通过这一步，`/api`路径(来源于`app/routes/overrides/route.api.php`)将以该用户的名称上传图像。

**改成这样是指定用户、指定相册**

```php
		$uploaded_id = CHV\Image::uploadToWebsite($source,'juanito', array('album_id'=>1)); 
```

#### 4）注册和登录页面显示公共头部和尾部

##### 修改 login.php 文件

需要修改三处，一处为头部引用代码，另一处为背景调用代码，还有一处是尾部调用代码。

**a. 修改头部引用代码**

查找：

```php
<?php G\Render\include_theme_file('head'); ?>
```

替换为：

```php
<?php G\Render\include_theme_header(); ?>
```

**b. 修改背景调用代码**

查找：

```php
<?php G\Render\include_theme_file('snippets/quickty/background_cover'); ?>
```

替换为：

```php
<?php G\Render\include_theme_file('snippets/homepage_cover_slideshow'); ?>
```

**c. 修改尾部代码**

查找：

```php
<?php G\Render\include_theme_file('snippets/quickty/top_left'); ?>
```

替换为：

```php
<div id="home-cover-footer">
    <?php _se('Powered by Chevereto')?>
</div>
```

##### 修改 header.php 文件

需要修改两处，一处修改 class 内容，另一处为修改 logo 地址。

**a. 修改 class 内容**

查找：

```php
if (G\get_route_name() == 'index') {
    $body_class = CHV\getSetting('homepage_style');
    if (function_exists('get_list')) {
        $list = get_list();
        $hasPrev = $list->has_page_prev;
        if ($hasPrev) {
            $body_class = '';
        } else {
            $top_bar_class = in_array(CHV\getSetting('homepage_style'), ['landing', 'split']) ? 'black' : get_theme_top_bar_color();
        }
    } else {
        $top_bar_class = 'black';
    }
}
```

在后面添加：

```php
// 给 body 和 header 指定样式名称，跟首页保持一致，从而达到首页的头部效果
else if (G\get_route_name() == 'login' or G\get_route_name() == 'signup') {
    $body_class = 'full--wh landing'; 
    $top_bar_class = 'transparent black'; 
}
```

**b. 修改 logo 地址**

查找：

```php
if ($body_class && G\get_route_name() == 'index' and in_array(CHV\getSetting('homepage_style'), ['landing', 'split'])) {
    $logo_header .= '_homepage';
}
```

在后面添加：

```php
// 给 LOGO 指定样式名称，跟首页保持一致，从而达到首页的 LOGO 效果
else  if ($body_class && (G\get_route_name() == 'login' or G\get_route_name() == 'signup') and in_array(CHV\getSetting('homepage_style'), ['landing', 'split'])) {
    $logo_header .= '_homepage';
}
```

#### 5）Chevereto图床程序上传大图片失败Server error(Internal server error) 解决方法

很多人在使用上传图片时就一部分上传的时候提示:Server error（internal server error），特别是上传大文件的图片以及很多图片的时候，这个错误就简直了，因为他提示错误之后，有的图片会继续上传，有的不会，然后你就不知道你到底上传了什么图片，没上传什么图片。。。

上传多张图片是出错，或者上传单个大图片（7MB-10MB以上图片）时也会提示 Server error（internal server error），像这种情况我们需要修改一下PHP配置的数值：

```php
max_execution_time
max_input_time
memory_limit
post_max_size
upload_max_filesize
```

这个数值要根据自己服务器配置来调，服务器配置低的不要调太高。

#### 6）添加邮件模板

上传邮件模板文件至 Chevereto 主题 `Peafowl/overrides/mails/` 文件目录下即可，或者直接替换掉`mails` 目录亦可。

**目前已支持以下模板**

- 账号更换邮箱
- 新账户注册验证
- 账户重置密码
- 新用户注册欢迎

**更改邮件模板头图**

打开邮件模板文件，找到以下代码，替换为你自己的图片链接。

```php
$body_arr  = [ // Mail body array (easier to edit)
'Backimg' => 'https://resbeta.com/images/2019/02/22/365027cf0b5e911c3212750373c9f684.md.jpg',//修改此处图片链接即可
.........
];
```

**文件下载**

https://ola.niege.ml/t/DGO8KG

#### 7）其他

[Chevereto也能用QQ、GitHub、微博登陆啦 - 松鼠の博客 (doge.uk)](https://doge.uk/coding/chevereto-qq-login.html)

[Chevereto 更改图像预览快捷键 - 松鼠の博客 (doge.uk)](https://doge.uk/coding/chevereto-change-image-preview-shortcut.html)
