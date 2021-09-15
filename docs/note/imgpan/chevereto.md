# 宝塔面板安装Chevereto图床程序及其常见问题

## 关于Chevereto

Chevereto是一个可以帮助你建立自己的图像分享网站（图床）的应用程序，我们的目标是可以让世界上的任何一个人都可以建立自己的图像共享平台。我们坚定不移的为那些想要可定制的白标图像共享服务的人建立一个真正的替代品。

> 白标：white-label 直译为白标，引申为不注重品牌宣传的产品。Whitelabel致力于研发具有新功能、外形时尚、操作简单的产品，消费者可以尽情享受高科技带来的完美体验。whitelabel不做品牌宣传，我们提倡产品价值的回归，让消费者购买的是产品真正的价值，剔除广告费等一切隐形费用，享受超高性价比。良好的品质和口碑是我们最好的宣传。(摘自百度百科)

官方网站：https://chevereto.com/

官方文档：https://chevereto.com/docs

中文文档：https://ch.cndrew.cn/

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

![](C:\Users\Administrator\Desktop\Snipaste_2021-09-15_17-59-19.jpg)

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

