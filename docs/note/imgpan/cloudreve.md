<h1 align="center">
  <br>
  <a href="https://cloudreve.org/" alt="logo" ><img src="https://raw.githubusercontent.com/cloudreve/frontend/master/public/static/img/logo192.png" width="150"/></a>
  <br>
  Cloudreve
  <br>
</h1>

<h4 align="center">支持多家云存储驱动的公有云文件系统.</h4>

<p align="center">
  <a href="https://travis-ci.com/github/cloudreve/Cloudreve/">
    <img src="https://img.shields.io/travis/com/cloudreve/Cloudreve?style=flat-square"
         alt="travis">
  </a>
  <a href="https://codecov.io/gh/cloudreve/Cloudreve"><img src="https://img.shields.io/codecov/c/github/cloudreve/Cloudreve?style=flat-square"></a>
  <a href="https://goreportcard.com/report/github.com/cloudreve/Cloudreve">
      <img src="https://goreportcard.com/badge/github.com/cloudreve/Cloudreve?style=flat-square">
  </a>
  <a href="https://github.com/cloudreve/Cloudreve/releases">
    <img src="https://img.shields.io/github/v/release/cloudreve/Cloudreve?include_prereleases&style=flat-square">
  </a>
</p>

![Screenshot](https://raw.githubusercontent.com/cloudreve/docs/master/images/homepage.png)

## ⚙️简介

> 官网：https://cloudreve.org/
>
> github：https://github.com/cloudreve/Cloudreve
>
> 下载：https://github.com/cloudreve/Cloudreve/releases
>
> 文档：https://docs.cloudreve.org
>
> 演示：[https://pan.love2wind.com](https://pan.love2wind.com/)

Cloudreve 是个公有网盘程序，你可以用它快速搭建起自己的网盘服务，公有云/私有云都可。作者用了六个月的时间，把 Cloudreve 用 Go 语言重构了一遍，除了修复 V2 版本被诟病很多的 Bug 外，还增加了很多令人兴奋的新特性：[宝塔面板Cloudreve+Aria2配置离线下载 - 大鸟博客 (daniao.org)](https://www.daniao.org/13249.html)

## :sparkles: 特性

* :cloud: 支持本机、从机、七牛、阿里云 OSS、腾讯云 COS、又拍云、OneDrive (包括世纪互联版) 作为存储端
* :outbox_tray: 上传/下载 支持客户端直传，支持下载限速
* 💾 可对接 Aria2 离线下载
* 📚 在线 压缩/解压缩、多文件打包下载
* 💻 覆盖全部存储策略的 WebDAV 协议支持
* :zap: 拖拽上传、目录上传、流式上传处理
* :card_file_box: 文件拖拽管理
*  :family_woman_girl_boy:   多用户、用户组
* :link: 创建文件、目录的分享链接，可设定自动过期
* :eye_speech_bubble: 视频、图像、音频、文本、Office 文档在线预览
* :art: 自定义配色、黑暗模式、PWA 应用、全站单页应用
* :rocket: All-In-One 打包，开箱即用
* 🌈 ... ...

## ⚗️准备

安装之前你需要准备好环境：

1. 宝塔面板安装好（宝塔服务器面板，一键全能部署及管理，送你3188元礼包，点我领取https://www.bt.cn/?invite_code=MV9mbmFramU=）
2. 在宝塔面板安装nginx+mysql并启动成功
3. 域名一个（任意域名）
4. 在宝塔面板里新建网站和mysql数据库

## 🛠️安装和部署

#### 3、命令安装

SSH登录到服务器，复制并执行下面的命令即可完成安装。

**注意**：版本一直迭代，需要到下载页面获取最新版本的程序

```
cd /opt   #进入安装目录
wget  https://github.com/cloudreve/Cloudreve/releases/download/3.2.0/cloudreve_3.2.0_linux_amd64.tar.gz   #远程拉取cloudreve，这里替换成最新版
tar -zxvf cloudreve_3.2.0_linux_amd64.tar.gz   #解压获取到的主程序
chmod +x ./cloudreve  #赋予执行权限
./cloudreve   #启动 Cloudreve
```

![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-1.png)

Cloudreve 在首次启动时，会创建初始管理员账号，请注意保管管理员密码，此密码只会在首次启动时出现。如果您忘记初始管理员密码，需要删除同级目录下的“cloudreve.db”，重新启动主程序以初始化新的管理员账户。

Cloudreve 默认会监听“5212”端口。你可以在浏览器中访问“http://服务器IP:5212”进入 Cloudreve。如果宝塔面板需要在安全中放行“5212”端口。注意用默认的管理账号和密码登录。

#### 4、宝塔面板安装

以上步骤是在命令环境下执行的，其实如果我们用宝塔的话，不需要在命令环境下执行，这里简单介绍下。

1）新建好网站后，下载程序到自己的网站根目录，然后解压缩。

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/coudreve-32-1.png)](https://www.daniao.org/wp-content/uploads/2020/03/coudreve-32-1.png)

2）设置网站根目录下的<cloudreve>具有写权限，你可以设置为www、755~~

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/coudreve-32-1-1.png)](https://www.daniao.org/wp-content/uploads/2020/03/coudreve-32-1-1.png)

下面就可以设置进程守护即可启动程序了。

#### 5、进程守护

以上步骤操作完后，你可能需要一些更为具体的配置，才能让Cloudreve更好的工作，宝塔面板我们可以使用Supervisor管理器来设置进程守护，具体流程请参考下面的配置流程。

**1）安装Supervisor管理器**

软件商店→系统工具 ，找到Supervisor管理器安装即可。

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-2.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-2.png)

**2） 添加守护进程**

打开Supervisor管理器添加守护进程，看图：

注意，运行目录我们一般放在网站根目录，本教程放在了opt目录。这里直接注意一下。

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-3.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-3.png)

**注意**：路径修改为自己的。添加完成后，守护进程就会启动成功，如图：

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-4.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-4.png)

**注意**：设置守护进程之前，请先停止掉命令模式。

**3）管理员账号和密码**

进程守护之后，我们需要获取管理员的账号和密码，可以在Supervisor管理器的日志查看中看到你的账号和密码。

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/coudreve-32-3.png)](https://www.daniao.org/wp-content/uploads/2020/03/coudreve-32-3.png)

#### 6、域名访问

新建网站，之后在网站设置中，配置反向daili，如图：

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-5.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-5.png)

#### 7、效果展示

现在就可以用域名打开Cloudreve 访问了：

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-8.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-8.png)

 

管理面板：

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-9.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-9.png)

 

支持的存储策略：

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-10.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-10.png)

添加oneindex存储策略时详细的引导：

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-11.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-11.png)

创建WebDAV：

[![宝塔面板安装Cloudreve V3(go版本) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-12.png)](https://www.daniao.org/wp-content/uploads/2020/03/Cloudreve-V3-go-12.png)

注意：目前 V3 仍处于 RC 版本阶段，V2版本的升级措施会随着正式版一起发布。

#### 8、一些细节

首次启动时，Cloudreve 会在同级目录下创建名为“conf.ini”的配置文件，你可以修改此文件进行一些参数的配置，保存后需要重新启动 Cloudreve 生效。

默认情况下，Cloudreve 会使用内置的 SQLite 数据库，并在同级目录创建数据库文件“cloudreve.db”，如果您想要使用 MySQL，请在配置文件中加入以下内容，并重启 Cloudreve。

```
[Database]#数据库类型，目前支持 sqlite | mysqlType = mysql#用户名User = root#密码Password = root#数据库地址Host = 127.0.0.1#数据库名称Name = v3#数据表前缀TablePrefix = cd
```

注意：更换数据库配置后，Cloudreve 会重新初始化数据库，原有的数据将会丢失。

#### 9、最后

从使用体验来看，效果很不错，功能强大，支持存储种类也多，唯一不足的地方竟然不支持Google Drive 。作者更是说目前不支持，未来也不会支持。

安装真的是很简单了，比之前的v2版本安装简单的多。不过目前还是测试版，所以有bug是很正常的。

场景使用：可以使用 Cloudreve 搭建个人用网盘、文件分享系统，亦或是针对大小团体的公有云系统。