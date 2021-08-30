# 简 介

ShareList 是一个易用的网盘工具，支持快速挂载 GoogleDrive、OneDrive ，可通过插件扩展功能。

> **项目地址：** https://github.com/reruin/sharelist
>
> **文档： **https://reruin.github.io/sharelist/docs/#/zh-cn/
>
> **DEMO：** https://list.niege.ml

# 安装

Sharelist支持多种安装方式。

## 脚本安装

脚本安装适合不熟悉NodeJs的用户，执行命令后将自动安装NodeJs环境，并在当前目录（执行命令的目录）安装sharelist。

```bash
wget --no-check-certificate -qO-  https://raw.githubusercontent.com/reruin/sharelist/master/netinstall.sh | bash
```

访问 `http://localhost:33001` 即可进入 WebDAV 目录 `http://localhost:33001/webdav`

sharelist自带更新脚本，在sharelist目录内执行 `update.sh`即可自动更新。

!> Sharelist需要NodeJS运行环境(>=8.0)，一些早期的发行版可能无法被支持。此脚本不支持Windows。

## 手动安装

如果已有NodeJs环境，或者需要在windows下安装，可选择手动安装。

将[项目仓库](https://github.com/reruin/sharelist)克隆到本地，

```
#下载源码安装
git clone https://github.com/reruin/sharelist.git
```

进入项目目录执行:

```bash
cd sharelist
npm install
npm install pm2 -g

pm2 start app.js --name sharelist --env prod
pm2 save
pm2 startup
```

更新

```bash
bash update.sh
```

## Docker

```bash
docker run -d -v /etc/sharelist:/sharelist/cache -p 33001:33001 --name="sharelist" reruin/sharelist
```

## Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/reruin/sharelist-heroku)

## Kubesail

[![Deploy](https://img.shields.io/badge/deploy%20to-kubesail-blue?style=for-the-badge)](https://kubesail.com/template/reruin/sharelist)

# 初始化

安装完成首次访问 `http://localhost:33001`地址，将进入初始化界面。

#### 口令

这是个必填项，此口令用于登录sharelist的管理后台。

#### 网站标题

自定义的网站标题。

#### 虚拟路径

指挂载内容，默认挂载了当前项目目录。

# 挂载源

sharelist通过插件支持多种挂载源。从`后台管理`->`虚拟路径`，选择挂载源，输入挂载的名称和挂载路径即可。

!> 各网盘的挂载方式都不相同，具体挂载方法参考[官方文档挂载源设置](https://reruin.github.io/sharelist/docs/#/zh-cn/plugins/README)

 ![001.png](https://i.loli.net/2020/10/12/DAzubBWSkPGTCEq.png)

!> 还有更多高级设置文档里写的都很详细，请参考[官方文档高级设置](https://reruin.github.io/sharelist/docs/#/zh-cn/advance?id=smb)

# Q&A

## 🍅天翼云登录错误

打开`sharelist/plugins/drive.189cloud.js`

**查找（大概在133行）**

`https://cloud.189.cn/udb/udb_login.jsp?pageId=1&redirectURL=/main.action`

**替换为**

`https://cloud.189.cn/api/portal/loginUrl.action?redirectURL=https://cloud.189.cn/web/redirect.html`

**在SSH终端输入下面命令重启PM2**

`pm2 restart all`



# 挂载设置

## 前言

ShareList 是一个易用的网盘工具，支持快速挂载 GoogleDrive、OneDrive、等网盘，可通过插件扩展功能。可通过插件扩展功能。不占服务器空间；支持直链下载；在线预览（图片、视频、音频）

目前支持：GoogleDrive、OneDrive（含世纪互联）、天翼云盘（含企业版家庭版）、和彩云、本地文件、Github、蓝奏云、H5ai、WebDAV、SFTP等

与非门云盘演示：[https://drive.raycns.com](https://pan.ahfi.cn/)

作者Github：https://github.com/reruin/sharelist

## 特点

- 多种网盘系统快速挂载。
- 支持虚拟目录和虚拟文件。
- 支持目录加密。
- 插件机制。
- 国际化支持。
- WebDAV导出。

## 如何安装-脚本安装

```shell
#1.Debian/Ubuntu系统（看系统）
apt-get -y install git

#1.CentOS/RHEL系统（看系统）
yum -y install git

#2.下载源码
git clone https://gitee.com/Ling_N/sharelist.git   #国内
git clone https://github.com/reruin/sharelist.git  #国外
#3.执行安装
cd sharelist && bash install.sh
```

完成后，在宝塔中安全打开 33001端口，访问 [http://ip:33001，进入界面开始设置，（首次使用时将提示选在挂载源，选择挂载源，填入对应路径即可](http://ip:33001，进入界面开始设置，（首次使用时将提示选在挂载源，选择挂载源，填入对应路径即可/)。 系统内置了本地路径（FileSystem）挂载源，比如天翼云选择：账号密码挂载（Cookie方式））记住网盘文件夹要共享一下，不然会出现 500错误。

## 如何绑定域名-反向代理添加域名

在宝塔中添加一个新站点，只绑定域名就好，完成后访问域名等待解析成功
解析成功后，点网站列表右侧 设置，列表中的 反向代理，目标url设置为 [http://127.0.0.1:33001，发送域名自动生成，不用操作](http://127.0.0.1:33001，发送域名自动生成，不用操作/)

[![img](https://i.loli.net/2020/09/09/KFrMIi4kcjZ6nON.jpg)](https://i.loli.net/2020/09/09/KFrMIi4kcjZ6nON.jpg)

## 如何开启HTTPS

直接为这个站点配置SSL证书即可

## 挂载本地

如果按照我的方法安装，安装路径就是：root/sharelist
您可以在 sharelist文件夹内创建一个文件夹（最好为英文），然后在网站后台管理最下方，
挂载源：本地文件
虚拟路径：单填一个 /即挂载你整个硬盘，自己写路径
注意：如果后台打开了 开放上传功能，一定要加密目录，加密方法见下面

## 挂载天翼云盘

**1.账号密码挂载（Cookie方式）**
挂载源： 189 cookic/天翼云 账号登录版
挂载路径内容： /
填写 /，ShareList将自动开启挂载向导，按指示操作即可
注意：如果填写天翼云盘的账号密码显示错误，请确保输入的是正确的，然后 Ctrl+F5强制刷新一下或者等一会就好了

**2.API方式挂载**
挂载源： 天翼云 API版
挂载路径内容： /
填写 /，ShareList将自动开启挂载向导，按指示操作即可
注意：access_token每隔30天需手动更新一次，到期前24小时内访问对应路径时会有更新提示。

**3.天翼企业云盘挂载**
挂载源： 天翼企业云 账号密码版
挂载路径内容： /
然后访问主页，点击挂载天翼的文件夹，会让你输入天翼云盘的账号密码，输入即可。

## 挂载蓝奏云

挂载源： 蓝奏云/LanZou
挂载路径内容：password@folderId
password是你的链接访问密码，folderId是你的分享地址后面的bxxxxxxxx
比如：分享链接：https://lanzous.com/bxxxxxxx 访问密码：xxbb
挂载路径就是： xxbb@bxxxxxxxx
由于蓝奏云无法上传 .jpg.mp4等格式文件，可以在后面再加个 .ct上传
比如文件名为：ceshi.jpg，改为 ceshi.jpg.ct上传到蓝奏云即可
注意：蓝奏云vip版可以上传大于100M的文件，但大于100M的文件无法在ShareList访问！

## 挂载GoogleDrive

**1.使用分享ID挂载**
由plugins/drive.gd.js插件实现
挂载源：GDID挂载版
挂载路径内容：分享的文件ID

**2.使用官方API挂载**
由plugins/drive.gd.api.js插件实现。
挂载源：GD API版
挂载路径内容：//应用ID/root?client_secret=应用机钥&redirect_uri=回调地址&refresh_token=refresh_token/
建议填写 /，ShareList将自动开启挂载向导，按指示操作即可。

## 挂载OneDrive

**1.使用分享ID挂载**
由plugins/drive.od.js插件实现
挂载源：OD ID挂载版
挂载路径内容：分享的文件ID

**2.使用官方API挂载**
由plugins/drive.od.api.js插件实现。
挂载源：OD API版
挂载路径内容：OneDrive路径->应用ID|应用机钥|回调地址|refresh_token OneDrive路径/
建议填写 /，ShareList将自动开启挂载向导，按指示操作即可
对于不符合OneDrive安全要求的域名，将采用中转方式验证，查看中转页面
注意：由于onedrive修改了政策，个人Microsoft帐户已无法通过向导进行绑定。 需前往 Azure管理后台 注册应用并获取 app_id 和 app_secret 。

**3.使用官方API挂载世纪互联**
由plugins/drive.odc.api.js插件实现
挂载源：OD 世纪互联
挂载路径内容：//应用ID/路径?client_secret=应用机钥&redirect_uri=回调地址&refresh_token=refresh_token&tenant=组织名/
建议填写 /，ShareList将自动开启挂载向导，按指示操作即可
注意：组织名是指网盘访问链接中 https://***-my.sharepoint.cn/ 星号所示部分。

**4.挂载OneDrive For Business**
由plugins/drive.odb.js插件实现。
挂载源：* OD Business 非API
挂载路径内容：分享的url

## 目录加密

```txt
type: basic 
data: 
  - user1:111111 
  - user2:aaaaaa
```

basic是内置的验证方式，使用用户名密码对进行判断，上面的例子中可使用 user1的密码为 111111，user2的密码为 aaaaaa。

## 虚拟目录

在需创建虚拟目录处新建 目录名.d.ln文件。 其内容为 挂载源:挂载路径 如：创建虚拟目录指向本地 /root。

```txt
fs:/root
```

其中挂载源 fs表示本地磁盘，/root代表路径。
再如：创建虚拟目录指向GoogleDrive的某个共享文件夹

```txt
gd:0BwfTxffUGy_GNF9KQ25Xd0xxxxxxx
```

gd是GoogleDrive的挂载源标示，冒号后的是共享文件夹ID。