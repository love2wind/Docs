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

> 调用的时候后缀无所谓，

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



### 使用PHP文件自建API

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

