# 搭建随机图片的几种方法

!> 网络上有很多随机图片的API，看着挺不错，这里就整理几种方便搭建的方法，希望对大家有所帮助。

### 使用CF Worker搭建

#### 1.使用Github Repo

创建一个仓库，把图片传进去，然后在CF新建一个worker，把下面的代码贴进去。

```javascript
addEventListener(
  'fetch', event => {
    let url = new URL(event.request.url);
    var max=253;
    var min=1;
    url.host = 'raw.githubusercontent.com';
    url.pathname = 'usernamenotfount/wssbz/master/'
     + Math.floor(Math.random()*(max-min+1)+min) + '.jpg';
    let request = new Request(url, event.request);
    event.respondWith(
      fetch(request)
    )
  }
)
```

**修改里面的几个参数：**

- 仓库的地址：`usernamenotfount/wssbz/master/` 将这部分改成你的仓库
- 图片的数量：`var max=253` 将这部分改成你上传的图片数量
- 如果你使用其他服务器，可以改 `raw.githubusercontent.com`为对应的域名

> 演示：

#### 2.使用图片直链

将你的图片上传到图床并获取直链地址，然后在CF新建一个worker，把下面的代码贴进去。

```javascript
addEventListener('fetch', event => {
    event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {

	var background_urls = [
	'https://w.wallhaven.cc/full/ey/wallhaven-eymzjk.jpg',
	'https://w.wallhaven.cc/full/j8/wallhaven-j8rk95.png'
	]
	var index = Math.floor((Math.random()*background_urls.length));
	res = await fetch(background_urls[index])
    return new Response(res.body, {
        headers: { 'content-type': 'image/jpeg' },
    })
}
```

替换代码中的 `background_urls` 图片直链为你的直链就好

> 演示：https://autoimg.love2wind.workers.dev/img.jpg

### 使用PHP文件自建API

#### 1.使用图片外链

> 创建文件img.txt用于存放图片地址，如

```http
https://cdn.jsdelivr.net/gh/Daibi-mua/jsdelivr@1.3/9.jpg
https://cdn.jsdelivr.net/gh/Daibi-mua/jsdelivr@1.3/8.jpg
https://cdn.jsdelivr.net/gh/Daibi-mua/jsdelivr@1.3/3.png
```

> 创建index.php

```php
<?php
//存有美图链接的文件名img.txt
$filename = "img.txt";
if(!file_exists($filename)){
    die('文件不存在');
}
 
//从文本获取链接
$pics = [];
$fs = fopen($filename, "r");
while(!feof($fs)){
    $line=trim(fgets($fs));
    if($line!=''){
        array_push($pics, $line);
    }
}
 
//从数组随机获取链接
$pic = $pics[array_rand($pics)];
 
//返回指定格式
$type=$_GET['type'];
switch($type){
 
//JSON返回
case 'json':
    header('Content-type:text/json');
    die(json_encode(['pic'=>$pic]));
 
default:
    die(header("Location: $pic"));
}
 
?>
```

**将 `img.txt` 和 `index.php` 放在同一个网站目录下，通过访问 `域名/index.php` 即可**

> 演示：https://api.imgsrc.xyz/img.php

#### 2.使用服务器图片

利用PHP搭建一个属于自己的随机图片API方便调用，同时可隐藏真实图片地址，注意：图片必须存储在PHP服务器上。

##### 示例

https://tvv.tw/xjj/meinv/ct.html //该网页用的下面的API。

https://cf.cdn.xiazai.de/api/images //直接访问API无法显示图片。

##### 特性

- 完全隐藏图片文件的真实地址
- 支持调用域名白名单
- 支持多文件夹分类目录
- 前端调用支持使用随机数载入

##### 部署

https://github.com/galnetwen/Random-Image

1. 下载代码，解压至你域名文件夹根目录或者子目录
2. 开启 Apache 或者 Nginx 的伪静态功能
3. 访问：你的域名/images
4. 大功告成

##### 配置

打开 images.php 文件，添加域名白名单与默认文件夹即可。 照葫芦画瓢，不用多说了吧。

```
<?php
error_reporting(E_ERROR);
require_once 'imgdata.php';
$karnc = new imgdata();
 
/**
 * 遍历获取目录下的指定类型的文件
 * @param $path
 * @param array $files
 * @return array
 */
function getfiles($path, $allowFiles, &$files = array()) {
    if (!is_dir($path)) return null;
    if (substr($path, strlen($path) - 1) != '/') $path .= '/';
    $handle = opendir($path);
    while (false !== ($file = readdir($handle))) {
        if ($file != '.' && $file != '..') {
            $path2 = $path . $file;
            if (is_dir($path2)) {
                getfiles($path2, $allowFiles, $files);
            } else {
                if (preg_match("/\.(" . $allowFiles . ")$/i", $file)) {
                    $files[] = substr($path2, strlen($_SERVER['DOCUMENT_ROOT']));
                }
            }
        }
    }
    return $files;
}
 
/**
 * 域名白名单校验函数
 * @param $domain_list
 * @return true/false
 *在下面修改为你的网站域名，在下面列表中的网站才能调用API
 */
function checkReferer($domain_list = array(
    'haremu.com',
    'acg.sx'
)) {
    $status = false;
    $refer = $_SERVER['HTTP_REFERER']; //前一URL
    if ($refer) {
        $referhost = parse_url($refer);
        /**来源地址主域名**/
        $host = strtolower($referhost['host']);
        if ($host == $_SERVER['HTTP_HOST'] || in_array($host, $domain_list)) {
            $status = true;
        }
    }
    return $status;
}
 
//列出指定目录下的图片
$CONFIG = array();
$CONFIG['imageManagerAllowFiles'] = array(".png", ".jpg", ".jpeg", ".gif", ".bmp");
 
$base_Path = '/picture/'; //图片默认主目录
$category = 'a'; //图片默认分类目录
 
if ($_GET['folder']) {
    $folder = trim($_GET['folder']);
    $CONFIG['imageManagerListPath'] = $base_Path . $folder . '/';  //有GET访问的分类目录
} else {
    $CONFIG['imageManagerListPath'] = $base_Path . $category . '/'; //无GET访问的默认目录
}
 
$allowFiles = $CONFIG['imageManagerAllowFiles'];
$path = $CONFIG['imageManagerListPath'];
 
$allowFiles = substr(str_replace(".", "|", join("", $allowFiles)), 1);
 
//获取文件列表
$path = $_SERVER['DOCUMENT_ROOT'] . (substr($path, 0, 1) == "/" ? "" : "/") . $path;
$files = getfiles($path, $allowFiles);
if (!count($path)) {
    return "抱歉，没有找到匹配的文件！";
}
 
//获取指定范围的列表
$len = count($files);
for ($i = 0, $list = array(); $i < $len; $i++) {
    $list[] = $files[$i];
}
 
$rand = array_rand($list, 1);
$img = $list[$rand];
$imgFile = $_SERVER['DOCUMENT_ROOT'] . (substr($list[$rand], 0, 1) == "/" ? "" : "/") . $img;
$imgNot = $_SERVER['DOCUMENT_ROOT'] . '/' . 'nico.gif'; //无授权域名图片
$refer = $_SERVER['HTTP_REFERER']; //前一URL
 
//存在前一URL
if ($refer) {
    if (!checkReferer()) {
        $karnc->getdir($imgNot);
        $karnc->img2data();
        $karnc->data2img();
        die;
    } else {
        $karnc->getdir($imgFile);
        $karnc->img2data();
        $karnc->data2img();
        die;
    }
} else {
    //直接访问API地址
    $imgWeb = file_get_contents('imgweb.html');
    echo $imgWeb;
    die;
}
?>
```

**多文件夹说明：** 第二个文件夹无需配置，直接使用 URL 传递参数即可。

比如： 默认文件夹的分类，调用的域名是：“ 你的域名/images ”
其它文件夹的分类，调用是域名是：“ 你的域名/images/文件夹名 ”

注意！ 若要使用随机数调用，必须启用 Apache 或者 Nginx 的伪静态功能，否则空白输出。
Nginx 用户需要手动添加 nginx.conf 文件里面的伪静态规则到你的域名配置中去……

```
rewrite ^/images$ /images.php last;
rewrite ^/images/(.*?)$ /images.php?folder=$1 last;
#下面是子目录例子：
rewrite ^/api/images$ /api/images.php last;
rewrite ^/api/images/(.*?)$ /api/images.php?folder=$1 last;
```

Apache伪静态

```
<IfModule mod_rewrite.c>
 
    RewriteEngine On
 
    RewriteRule ^images$ images.php [L,QSA]
    RewriteRule ^images/(.*?)$ images.php?folder=$1 [L]
 
</IfModule>
```

使用随机数载入的情况通常在一个页面多次调用随机图的时候，比如首页文章列表，否则图片都是一样的。

随机数载入方式：“ 你的域名/images?随机数 ” ，就是原有 URL 上添加一个英文问号和任意随机数。

示例：

```
<img src="https://cf.cdn.xiazai.de/api/images">
<img src="https://cf.cdn.xiazai.de/api/images/acg">
<img src="https://cf.cdn.xiazai.de/api/images?d8c196951e5bbf3edd158de4">
<img src="https://cf.cdn.xiazai.de/api/images/acg?9f0d34f8ee6f96b56d8902d1">
```

