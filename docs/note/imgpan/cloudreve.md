
![home](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/dd239c7b317b0e7171891b415cb793d0.webp)

## ⚙️简介

Cloudreve 可以让您快速搭建起公私兼备的网盘系统。Cloudreve 在底层支持不同的云存储平台，用户在实际使用时无须关心物理存储方式。你可以使用 Cloudreve 搭建个人用网盘、文件分享系统，亦或是针对大小团体的公有云系统。

> **官网：**https://cloudreve.org/
>
> **github：**https://github.com/cloudreve/Cloudreve
>
> **下载：**https://github.com/cloudreve/Cloudreve/releases
>
> **文档：**https://docs.cloudreve.org

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

## 🛠️部署

### 1.命令安装

SSH登录到服务器，复制并执行下面的命令即可完成安装。

```shell
#进入安装目录
cd /opt

#下载最新版cloudreve，记得替换成最新版地址
wget  https://github.com/cloudreve/Cloudreve/releases/download/3.3.2/cloudreve_3.3.2_linux_arm64.tar.gz   

#解压获取到的主程序
tar -zxvf cloudreve_VERSION_OS_ARCH.tar.gz

# 赋予执行权限
chmod +x ./cloudreve

# 启动 Cloudreve
./cloudreve
```

![命令安装) – 支持六大云存储存/OneDrive世纪互联/aria2等](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/cbf72a57670bc5384293dac3cf265c69.webp)

就是这么简单，几行命令就部署完成了。

Cloudreve 在首次启动时，会创建初始管理员账号，请注意保管管理员密码，此密码只会在首次启动时出现。如果您忘记初始管理员密码，需要删除同级目录下的“**cloudreve.db**”，重新启动主程序以初始化新的管理员账户。

Cloudreve 默认会监听 `5212` 端口。你可以在浏览器中访问 `http://服务器IP:5212` 进入 Cloudreve。如果宝塔面板需要在安全中放行 `5212` 端口。注意用默认的管理账号和密码登录。

### 2.宝塔面板安装

鉴于现在大家多用宝塔面板部署管理网站，这里就把宝塔面板下的cloudreve部署方法再说一下。

#### 1) 环境准备

1. 安装好宝塔面板的VPS一台。（宝塔服务器面板，一键全能部署及管理，送你3188元礼包，点我领取https://www.bt.cn/?invite_code=MV9mbmFramU=）
2. 在宝塔面板里部署好环境，Nginx+Mysql并成功启动。
3. 安装Supervisor管理器（**软件商店→系统工具 ，找到Supervisor管理器安装**）
4. 任意域名一个（可选）
5. 在宝塔面板里新建网站和mysql数据库

#### 2) 下载和权限

- 新建好网站后，进入网址目录，远程下载程序到自己的网站根目录，然后解压缩。

- 将解压后根目录下 `cloudreve>`  文件权限设置成www、755，如下图所示。

![下载和设置权限](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/059c692fc05ff3a1526863db1bbb083b.webp)

#### 3) 进程守护

下面我们就可以通过向宝塔面板的Supervisor管理器添加守护进程来启动并监控Cloudreve，具体流程请参考下图。

![添加守护进程](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/96c27b78ff8c8b61f28f84b836a87cd0.webp)

##### 添加流程：

?> 宝塔面板——软件商店——找到Supervisor——点击设置——Supervisor管理器——添加守护进程

##### 注意：

- 运行目录我们一般放在网站根目录，大家根据自己实际情况改动
- 启动命令这里填`cloudreve`即可，不过推荐填写完整的绝对路径，不然容易出现各种问题
- 进程守护之后，可以在Supervisor管理器的日志查看中看到你的账号和密码

到这里，宝塔面板的Cloudreve已经部署完成了，可以访问http://你的服务器IP:5212来访问了，那我们怎么用域名访问呢？这就要看下一步要做的了。

#### 4) 域名访问

在网站设置中添加反向DAILI后你就可以使用域名访问Cloudreve网站了，见下图。

![反向DAILI](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/098cf20f5a1b0f3754a314f750757215.webp)

#### 5) 后台设置

现在就可以用域名打开Cloudreve，使用管理员账号密码登录后进入管理后台，设置好各项参数后就算完成Cloudreve部署了。

![Snipaste_2021-08-12_17-10-31](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/8234fbc8263daafe775b7ad44758e4b2.webp)

## 存储策略对比

Cloudreve支持以下存储策略：本机、从机、七牛、腾讯OSS、阿里COS、又拍云、OneDrive、S3。具体的存储策略设置按照后台的设置流程操作就好，没有什么难度，这里贴一下官网的对比图。

#### **基本对比**

|                | 本机 | 从机 | 七牛 | OSS  | COS  | 又拍云 | OneDrive | S3   |
| -------------- | ---- | ---- | ---- | ---- | ---- | ------ | -------- | ---- |
| 上传           | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 下载           | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 复制           | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 移动           | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 普通预览       | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| Office 预览    | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 删除           | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 缩略图         | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ❌    |
| 打包下载       | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 真实文件名下载 | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ❌        | ✅    |
| 理论最大文件   | 无限 | 无限 | 无限 | 5GB  | 5GB  | 150GB  | 未知     | 未知 |
| 公网接入要求   | 无   | 无   | 需要 | 需要 | 需要 | 需要   | 需要     | 需要 |

#### **高级功能**

|          | 本机 | 从机 | 七牛 | OSS  | COS  | 又拍云 | OneDrive | S3   |
| -------- | ---- | ---- | ---- | ---- | ---- | ------ | -------- | ---- |
| 离线下载 | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 下载限速 | ✅    | ✅    | ❌    | ✅    | ✅    | ❌      | ❌        | ❌    |
| 直链获取 | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ❌    |
| 解压缩   | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
| 压缩     | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅        | ✅    |
|          |      |      |      |      |      |        |          |      |

#### **流量路径**

|                      | 本机 | 从机 | 七牛 | OSS  | COS  | 又拍云 | OneDrive      | S3   |
| -------------------- | ---- | ---- | ---- | ---- | ---- | ------ | ------------- | ---- |
| Web 上传客户端直传   | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | >= 4MB 时直传 | ✅    |
| 下载直传             | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅             | ✅    |
| 打包下载/压缩/解压缩 | 直传 | 中转 | 中转 | 中转 | 中转 | 中转   | 中转          | 中转 |
| 离线下载             | 直传 | 中转 | 中转 | 中转 | 中转 | 中转   | 中转          | 中转 |
| 文本编辑             | 直传 | 中转 | 中转 | 中转 | 中转 | 中转   | 中转          | 中转 |
| WebDAV 上传直传      | ✅    | ❌    | ❌    | ❌    | ❌    | ❌      | ❌             | ❌    |
| WebDAV 下载直传      | ✅    | ✅    | ✅    | ✅    | ✅    | ✅      | ✅             | ✅    |

## 写在最后

整体来说Cloudreve还是很强大的，功能丰富，运行稳定，是自建网盘系统的不错选择。你还可以安装Aria2后配合Cloudreve的离线下载将文件下载到Onedrive里在线观看等，更多惊喜就等你来发掘了。

