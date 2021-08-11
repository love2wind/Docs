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