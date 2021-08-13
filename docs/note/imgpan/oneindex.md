![头图](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/7d0bcf745c2c67572f6b79785890c16c.webp)

OneIndex是一款专门映射挂载 **Onedrive** 网盘的一个开源程序。可以将Onedrive存储的文件通过列表的的方式进行展示，可以进行直链下载、**在线播放视频、音乐等媒体文件**！不占用服务器空间，不走服务器的流量！几乎是零成本搭建自己的专用网盘。

**特点：**

- 响应式，支持小屏设备

- 视频、音乐在线播放

- 图片在线预览

- 代码在线查看

- 支持文件夹加密

- 支持自定义头部、底部显示

- 支持文件上传

## 准备工作

1）一台支持PHP+mysql的VPS，虚拟机也是可以的

2）一个OneDrive账号，微软个人账号15G，或者申请E5账号5T也是可以的

3）(可选)一个域名用于解析

## 宝塔面板安装

原作者已经删库了，大家可以在github上搜索`onedrive`，总会有人fork下来的😍，当然，你也可以 [从这个地址](https://niege.ml/od5t/1index.zip) 下载我的备份文件。

**因为都是很基本的宝塔操作，这里就不放图了，大概给大家说下流程，大家可以看下面作者整个安装演示动图。**

1. 添加PHP站点：注意同时要新建Mysql数据库；
2. 上传或者远程下载Oneindex程序到网站根目录，解压压缩包；
3. 进入网站设置，申请免费的ssl证书并设置强制HTTPS；
4. 使用域名登入Oneindex首页会自动进入到安装步骤。

![安装步骤](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/320b7c71af20af8726ac90a7c918ce16.gif)

!> **后台的初始密码是 `oneindex` ,记得登录后修改密码哦。**

## 特殊文件实现功能  

`README.md`、`HEAD.md` 、 `.password`特殊文件使用

可以参考https://github.com/donwa/oneindex/tree/files

**在文件夹底部添加说明:** 

> 在 OneDrive 的文件夹中添加`README.md`文件，使用 Markdown 语法。

**在文件夹头部添加说明:** 

> 在 OneDrive 的文件夹中添加`HEAD.md` 文件，使用 Markdown 语法。

**加密文件夹:** 

> 在 OneDrive 的文件夹中添加`.password`文件，填入密码，密码不能为空。  

**直接输出网页:**

> 在 OneDrive 的文件夹中添加`index.html` 文件，程序会直接输出网页而不列目录。
> 配合 文件展示设置-直接输出 效果更佳。

## 设置伪静态

进入网站设置，点开伪静态标签，复制下面代码后保存，然后在oneindex后台设置将`去掉地址栏中的/?/`这个选项打开。

```nginx
if (!-f $request_filename){
    set $rule_0 1$rule_0;
}
if (!-d $request_filename){
    set $rule_0 2$rule_0;
}
if ($rule_0 = "21"){
    rewrite ^/(.*) /?/$1 last;
}
```

## 设置定时任务

!> **为了提高提高系统访问性能，我们需要定时刷新缓存，不然你存取的文件有的时候看不到，影响体验。我们可以直接用宝塔面板自带的定时任务来设置，分别是每小时刷新一次token 和 每十分钟后台刷新一遍缓存。**

进入宝塔面板计划任务，添加下面两个任务

1) **刷新token**

> 任务类型：Shell脚本 
>
> 任务名：每小时刷新一次token 
>
> 执行周期：每小时 0分钟 
>
> 脚本内容：php `你的网站目录路径`/one.php token:refresh 
>

2. **刷新缓存**

> 任务类型：Shell脚本 
>
> 任务名：每十分钟后台刷新一遍缓存 
>
> 执行周期：N分钟 10分钟 
>
> 脚本内容：php `你的网站目录路径`/one.php cache:refresh 

## 写在最后

Oneindex到这里就安装完成，你可以享用你的个人网盘了。oneindex算是最早的一个Onedrive列表程序，功能丰富，操作简洁，界面简洁，虽说现在各种列表程序层出不穷，但是还是有很多用户在继续使用，这里说个小技巧，在搜索引擎搜索`index of / – OneIndex`就能找到网友们搭建的网盘，也许你能发现一些好东西哦。😋