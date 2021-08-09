## ✨简介

**OlaIndex**一款 `OneDrive` 目录文件索引应用，基于优雅的 `PHP` 框架 `Laravel` 搭建，并通过 `Microsoft Graph` 接口获取数据展示，支持多类型帐号登录，多种主题显示，简单而强大。

- **项目地址：**https://github.com/WangNingkai/OLAINDEX

- **文档地址：**https://olaindex.js.org

- **演示地址：**https://ola.niege.ml

## ⚙️功能

> OneDrive 文件目录索引
>
> 支持多种资源即时预览
>
> 支持多账号

## 💖安装

本程序可以手动安装，也可使用docker安装，这里主要介绍下使用宝塔面板下手动安装的方法。

### ⚗️环境准备

1. 宝塔面板（宝塔服务器面板，一键全能部署及管理，送你3188元礼包，点我领取https://www.bt.cn/?invite_code=MV9mbmFramU=）
2. 在宝塔面板安装nginx+mysql+PHP7.0以上，并启动成功
3. 域名一个（任意域名）

### 🎉安装PHP扩展

?> 宝塔面板 - PHP设置 - 安装 - 安装扩展

- 安装`fileinfo` （必须）
- 安装 `opcache`  （可选、加速php运行）
- 安装 `redis` （可选）

![image-20210809012324024](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210809012324024.png)

!> 安装`fileinfo`有时会出错，尤其是小内存的机器，可以去宝塔工具箱设置一下swap，然后把nginx和mysql暂时先关闭，安装后再开启。

### 🎏禁用函数

?> 宝塔面板 - PHP设置 - 安装 - 禁用函数 - 函数 - 删除

关闭下列几个禁用的函数

-  `exec` 
- `shell_exec` 
-  `proc_open` 
- `putenv``
- ``proc_get_status`(这个有可能没有) 

![image-20210809014257767](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210809014257767.png)

禁用完了之后，记得重启一下`php`服务。

### 🍵安装Composer

宝塔面板已经默认自带了，但是为避免出错，我们进行饱和式设置。
接下来用ssh（不建议直接宝塔的ssh，这里用的是FinalShell）。

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344703362-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344703362-image.png)

```nginx
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ # 更换源为国内源，国外服务器可忽略此步骤curl -sS https://getcomposer.org/installer | php
```

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344733927-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344733927-image.png)

注：在执行第三行代码时，如果出现让你不要用`root`来操作的问题，可以参考下面的步骤。

添加一个用户（Debian为例）:

```nginx
adduser roy
```

执行命令后，根据提示操作即可。请务必设置一个用户密码（别忘记设置密码时你时看不到 ****** 的）。之后系统会询问你一些用户的附加信息，这些就可以无视，一路回车即可。

安装sudo功能:

sudo 就是在关键时刻，让普通账户临时获得 root 的神力，战力全开拯救世界。

```sql
apt update && apt install sudo
```

聪明的你大概已经发现，这一行命令其实是两个命令。前一半 `apt update` 你之前已经见过并且用过了，是去服务器刷新软件版本信息。后面的 `apt install` 就是这一次要用到的【安装命令】。两条连接在一起，就是让系统去【刷新可用的最新软件，然后安装最新版的sudo程序】。 `&&` 则是把两个命令连起来执行的意思。

把`roy`用户加入`sudo`名单里，让他有资格借用`root`的神力:

```nginx
visudo
```

在 `User Privilege Specification` 下加入一行 `roy ALL=(ALL) NOPASSWD: ALL` 即可。

> 注意：要特别说明的是`NOPASSWD`这个设置，它的意思是`roy`用户临时使用`root`权限时，不用额外输入密码。这与一般的安全建议相反。我之所以如此推荐，是因为很多新人不顾危险坚持使用`root`账号就是因为用`root`时不用重复输入密码、觉得轻松。“两害相权取其轻”，我认为【直接用`root`用户的风险】大于【使用`sudo`时不用输密码的风险】，所以做了以上的建议。
>
> 如果你希望遵守传统习惯、每次使用`sudo`时需要输入密码，那么这一行改成 `vpsadmin ALL=(ALL:ALL) ALL` 即可。

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344748923-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344748923-image.png)

### 🚀新建站点

宝塔面板内，新建一个站点，PHP版本就选刚才配置的对应版本，数据库不用创建，删除站点目录下的所有文件。

![image-20210809020205877](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210809020205877.png)

![image-20210809020403825](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210809020403825.png)

## 配置OLAINDEX

注意：这些命令要一行一行执行！

```perl
cd web目录   #例如我是cd /www/wwwroot/od.laoda.de
sudo git clone https://github.com/WangNingkai/OLAINDEX.git tmp #从github仓库拉取项目代码
sudo mv tmp/.git .   #进行整理
sudo rm -rf tmp     #删除缓存文件
sudo git reset --hard 
sudo composer install -vvv # 这里确保已成功安装 composer ，如果报权限问题，建议给予用户完整权限。直接用root运行。
sudo chmod -R 777 storage/* 
sudo chown -R www:www * # 此处 www 根据服务器具体用户组而定，如果是宝塔，直接运行就可以
composer run install-app # (此为自动安装，默认sqlite存储数据)
```

注意运行`composer install -vvv`的时候，用`root`或者`sudo`运行,否则会报错

```
vendor does not exist and could not be created
```

没有遇到其他问题的话，最后结果是这样的，默认账户`admin`,默认密码`123456`

## 配置网站

### 配置SSL

选择 Let’s Encrypt 申请，按要求填写申请，

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344849693-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344849693-image.png)

开启 SSL 后，选择强制 HTTPS

### 网址运行目录

如图：勾选取消 防跨站攻击(open_basedir) 将站点的运行目录改为 public 别忘了保存

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344863450-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344863450-image.png)

### 修改伪静态

选择 `Laravel 5`，保存

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344875529-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344875529-image.png)

### 修改配置文件

注释选定内容，防止图片出现404

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344889461-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344889461-image.png)

### 登陆

输入网址/admin，登陆就OK啦。

#### 后台设置

记得在这边设置一下，否则可能会报错。

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-30/1619795722055-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-30/1619795722055-image.png)

#### 具体如下

图片

```nginx
bmp jpg jpeg png gif
```

视频

```apache
mkv mp4 webm qlv TS
```

Dash视频

```nginx
avi mpg mpeg rm rmvb mov wmv asf ts flv TS
```

音频

```nginx
mp3 ogg wav flac ape
```

Office文档

```nginx
text json md
```

代码

```go
html htm css go java js ts sh php py
```

文件流

```bash
txt log
```

#### 关于密码文件夹的问题

根目录下的文件**要**加`/`

视频中设置了密码但是输入仍然无效，猜测是hux主题的问题，我换了simplex主题后，bug消失，其他主题也可以试试。

[![img](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344900239-image.png)](https://cdn.jsdelivr.net/gh/RalstonLiu/Mdnice3/2021-4-25/1619344900239-image.png)

#### 关于隐藏文件夹的问题

根目录下的文件**不要**加`/`

绑定好OD账户，就可以愉快得玩耍起来了。

OD账户不会绑定？额，自己先折腾一下，下一篇再和大家细讲吧。

### 参考

[官方文档](https://olaindex.js.org/#/install)

[宝塔面板部署Olaindex搭建自有网盘](https://lmqyu.cn/793.html)

[BT 面板安装 OLAINDEX 全方位指南](https://imwnk.cn/archives/bt-olaindex)

[Project X](https://xtls.github.io/documents/level-0/ch04-security/) （参考了添加用户的那部分内容）

[姨妈级安装教程！Olaindex——一款颜值贼高的OneDrive网盘直链项目 - 二十五画生 (laoda.de)](https://blog.laoda.de/archives/olaindex-install)

