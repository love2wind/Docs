## 简介

ImgURL是一款开源图床程序，首个版本诞生于2017年12月，经过重构 + 多个版本更新，目前已经相对稳定，现在正式发布ImgURL Pro专业版图床程序，满足更多用户需要。同时ImgURL社区版（开源版）将继续维护，但是功能有别于专业版，根据自己的需要选择即可。

!> ImgURL Pro 由 [小z博客](https://www.xiaoz.me/archives/13225) 开发

## 下载

ImgURL Pro 下载：https://pan.npapi.ml/l9w/Code/imgurl-pro.tar.gz

## 安装

**所需环境 & 安装教程：**https://www.yuque.com/helloz/imgurl-pro

**ImgURL Pro 专业版为收费程序，根据域名授权验证，本文章仅用于学习交流，建议尽量支持购买正版！**

## 禁用授权验证

**根据官方安装完成后访问域名会显示**
[![img](https://www.cooluc.com/usr/uploads/2020/08/3067493147.webp)](https://www.cooluc.com/usr/uploads/2020/08/3067493147.webp)

**接着在站点根目录创建密钥免授权补丁文件：`disable_key.php`**

```php
<?php
echo '<title>ImgURL Pro 禁用域名授权</title>';
$domain = $_SERVER['SERVER_NAME'];
$tld = explode('.', $domain);
$num = count($tld);
$domain = $tld[$num - 2] . '.' . end($tld);
$file_name = md5(base64_encode($domain)) . '.txt';
$keypath = 'data/'.$file_name;
$key = fopen("$keypath", "w") or die("无法写入密钥，请检查 ImgURL Pro 是否正确安装");
fwrite($key, md5($domain));
fclose($key);
echo '域名：' .$_SERVER['SERVER_NAME'] .' 授权成功';
?>
```

**通过你的域名访问补丁文件 ，如 `https://img.example.com/disable_key.php`**

密钥创建成功你将会看到提示 `域名：img.example.com 授权成功`

------

[![img](https://www.cooluc.com/usr/uploads/2020/08/4077312150.webp)](https://www.cooluc.com/usr/uploads/2020/08/4077312150.webp)





[![img](https://www.cooluc.com/usr/uploads/2021/09/2830715222.webp)](https://www.cooluc.com/usr/uploads/2021/09/2830715222.webp)



[ImgURL Pro图床专业版免授权安装 - Cooluc's Blog](https://www.cooluc.com/archives/83.html/comment-page-3#comments)

### 完毕！