# VScode安装配置记录

## 介绍

本文分享Vscode的下载、安装,以及配置，将采取三个步骤来进项详解。

## 下载

> **官网下载：**https://code.visualstudio.com/Download

选择对应系统的版本，本博客用windows系统，选择框框中的版本：



![20210810024221-2021-08-10](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/20210810024221-2021-08-10.png)
- 注意：解压到非系统盘（节约系统盘空间，也方便后面使用）
- 文件夹最好不要出现中文和空格，如：解压到D:\VSCode-win32-x64-1.31.1

## 安装

**直接运行`code.exe`即可**

![img](https://pic4.zhimg.com/v2-801b52b391f7ec9d9f1b26699c5803b3_b.jpg)![img](https://pic4.zhimg.com/v2-801b52b391f7ec9d9f1b26699c5803b3_r.jpg)

## 中文环境

### 1.下载安装中文语言包

点击左侧工具栏的extensions或者使用快捷键`Ctrl+Shift+X`，输入`chinese`，点击Install安装中文简体

![img](https://pic3.zhimg.com/v2-f73847edff6583edb043f4bc375840e2_b.jpg)![img](https://pic3.zhimg.com/v2-f73847edff6583edb043f4bc375840e2_r.jpg)

### 2.配置环境

使用快捷键`Ctrl+Shift+P`弹出查找命令框，输入`language`, 找到**Configure Display Language**，点击，选择**locale**属性为`zh-CN`，如下图所示：



![img](https://pic4.zhimg.com/v2-fcd57d3d2287164a14a84a12518b5a37_b.jpg)![img](https://pic4.zhimg.com/v2-fcd57d3d2287164a14a84a12518b5a37_r.jpg)

### 3.重启vscode



## 配置SOCKS5

翻阅[Chromium network settings](https://www.chromium.org/developers/design-documents/network-stack/socks-proxy),Chromium通过启动是增加以下命令行参数实现SOCKS代理设置

```c++
--proxy-server="socks5://myproxy:8080"
--host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE myproxy"
```

因此在本地VSCode快捷方式中目标参数增加以上命令项，即可实现VSCode的SOCKS5代理

```c++
C://****/Code.exe --proxy-server="socks5://myproxy:8080" --host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE myproxy"
```

## 配置HTTP Proxy

> 通过设置`http.proxy`的方法现已失效（只能在有限场景下提供支持）

1. VS Code 支持使用系统代理。

2. 为 VS Code 单独设置，避免改变系统代理带来的一些问题。

   在快捷方式中附加以下命令即可：

   ```c++
   --proxy-server="http://127.0.0.1:7890"
   # 将引号内容替换为自己代理服务器地址和端口
   ```

## MD侧边栏预览

Visual Studio Code 原生就支持高亮Markdown的语法，想要一边编辑一遍预览，有两种方法：

- `Ctrl + Shift + P` 调出主命令框，输入 `Markdown`，选择`Markdown: Open Preview to the Side`，就能调出实时预览框了。

- 先按`Ctrl + K`，然后放掉，紧接着再按`v`，也能调出实时预览框。

## 配置PicGO扩展
VSCode的 PicGo 是基于PicGo-Core开发的一款插件，这样的感觉就像在是在线编辑器里面的实时编辑的体验。

> 支持的图床有 微博图床 v1.0、七牛图床 v1.0、腾讯云COS v4\v5版本 v1.1 & v1.5.0、拍云 v1.2.0、GitHub v1.5.0、SM.MS v1.5.1、阿里云OSS v1.6.0、Imgur。

- 下载插件picgo
> 在VScode应用商店搜索`picgo`安装即可

- 扩展配置

> 打开配置，配置好图床参数即可

- 使用快捷键

## 使用

| 系统           | 从剪贴板上传图像 | 从资源管理器上传图像 | 从输入框上传图像 |
| -------------- | ---------------- | -------------------- | ---------------- |
| Windows / Unix | Ctrl + Alt + u   | Ctrl + Alt + e       | Ctrl + Alt + o   |
| macOS          | Cmd + Opt + u    | Cmd + Opt + e        | Cmd + Opt + o    |

