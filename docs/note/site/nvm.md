## 前言

最近由于想给博客文章图片加个水印，又不想用单独的软件每次都加水印，想到picgo好像有水印插件[picgo-plugin-watermark](https://github.com/fhyoga/picgo-plugin-watermark)，所以就兴冲冲的装起来，可在安装的时候发现无论怎么装都没反应。具体表现就是安装后显示已安装，可打开插件列表却找不到水印插件，重启picgo也不行。打开picgo的插件目录 `C:\Users\Administrator\AppData\Roaming\PicGo` ，使用命令 `npm install picgo-plugin-watermark` 直接安装还是一样，下载插件直接本地导入也行不通，无奈，在插件项目issues看了下发现好多人都是一样的问题，好像是和重命名插件和压缩插件冲突，卸载这两个插件再次重装还是一样的问题，而且我看了下，1.1.0版本作者就是专门解决了插件冲突的问题。这时发现有回复说降级node版本到10.24.0以后安装成功了，本着不折腾不会死的精神，就降级折腾一把吧。至此就有了今天这篇文，记录一下windows下的node.js版本管理软件nvm的安装设置过程。

## 安装nvm管理工具

如果你以前安装过node.js的话，请在控制面板卸载掉，然后删除以前的node安装目录，并且删除你以前配置的环境变量，最好重启一下机器再安装nvm会避免不少麻烦。

### 安装

首先关掉杀毒软件，不然会弹出警告！然后从官网下载最新安装包 https://github.com/coreybutler/nvm-windows/releases，解压得到 `nvm-setup.exe`， 运行此文件进行安装。（安装过程看下图）

> - 勾选 **`I accept the agreement`** 点击 `Next`；
> - 选择**nvm**安装路径**（这里一定要放在某个分区根目录，目录名称不能有中文、空格、符号，不然会报错）**，点击 `Next`；
> - 选择**node**安装路径**（这个倒是无所谓，不过尽量还是放在nvm目录的同级）**，点击 `Next`；
> - 点击 `Install` 安装，然后点击 `finish` 完成安装。
>

![](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/342d9de445689a0d291d1a0fa1af6e3b.webp)

##  安装切换node.js版本

### 验证nvm安装

WIN+R打开运行，输入 `cmd` ，打开命令行，输入 `nvm`  进行验证，没有问题的话就会返回下面的命令解释。

```c++
C:\Users\Administrator>nvm

Running version 1.1.8.

Usage:

  nvm arch                     : Show if node is running in 32 or 64 bit mode.
  nvm current                  : Display active version.
  nvm install <version> [arch] : The version can be a specific version, "latest" for the latest current version, or "lts" for the
                                 most recent LTS version. Optionally specify whether to install the 32 or 64 bit version (defaults
                                 to system arch). Set [arch] to "all" to install 32 AND 64 bit versions.
                                 Add --insecure to the end of this command to bypass SSL validation of the remote download server.
  nvm list [available]         : List the node.js installations. Type "available" at the end to see what can be installed. Aliased as ls.
  nvm on                       : Enable node.js version management.
  nvm off                      : Disable node.js version management.
  nvm proxy [url]              : Set a proxy to use for downloads. Leave [url] blank to see the current proxy.
                                 Set [url] to "none" to remove the proxy.
  nvm node_mirror [url]        : Set the node mirror. Defaults to https://nodejs.org/dist/. Leave [url] blank to use default url.
  nvm npm_mirror [url]         : Set the npm mirror. Defaults to https://github.com/npm/cli/archive/. Leave [url] blank to default url.
  nvm uninstall <version>      : The version must be a specific version.
  nvm use [version] [arch]     : Switch to use the specified version. Optionally use "latest", "lts", or "newest".
                                 "newest" is the latest installed version. Optionally specify 32/64bit architecture.
                                 nvm use <arch> will continue using the selected version, but switch to 32/64 bit mode.
  nvm root [path]              : Set the directory where nvm should store different versions of node.js.
                                 If <path> is not set, the current root will be displayed.
  nvm version                  : Displays the current running version of nvm for Windows. Aliased as v.
```

接下来我们输入命令 `nvm list available` 查看可用的node.js版本号，如果你知道你要下载那个版本这一步就不需要。这时国内用户还要设置下镜像地址，不然也会报错。

```shell
C:\Users\Administrator>nvm list available

|   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
|--------------|--------------|--------------|--------------|
|   16.10.0    |   14.17.6    |   0.12.18    |   0.11.16    |
|    16.9.1    |   14.17.5    |   0.12.17    |   0.11.15    |
|    16.9.0    |   14.17.4    |   0.12.16    |   0.11.14    |
|    16.8.0    |   14.17.3    |   0.12.15    |   0.11.13    |
|    16.7.0    |   14.17.2    |   0.12.14    |   0.11.12    |
|    16.6.2    |   14.17.1    |   0.12.13    |   0.11.11    |
|    16.6.1    |   14.17.0    |   0.12.12    |   0.11.10    |
|    16.6.0    |   14.16.1    |   0.12.11    |    0.11.9    |
|    16.5.0    |   14.16.0    |   0.12.10    |    0.11.8    |
|    16.4.2    |   14.15.5    |    0.12.9    |    0.11.7    |
|    16.4.1    |   14.15.4    |    0.12.8    |    0.11.6    |
|    16.4.0    |   14.15.3    |    0.12.7    |    0.11.5    |
|    16.3.0    |   14.15.2    |    0.12.6    |    0.11.4    |
|    16.2.0    |   14.15.1    |    0.12.5    |    0.11.3    |
|    16.1.0    |   14.15.0    |    0.12.4    |    0.11.2    |
|    16.0.0    |   12.22.6    |    0.12.3    |    0.11.1    |
|   15.14.0    |   12.22.5    |    0.12.2    |    0.11.0    |
|   15.13.0    |   12.22.4    |    0.12.1    |    0.9.12    |
|   15.12.0    |   12.22.3    |    0.12.0    |    0.9.11    |
|   15.11.0    |   12.22.2    |   0.10.48    |    0.9.10    |

This is a partial list. For a complete list, visit https://nodejs.org/download/releases
```

### 设置nvm镜像，提高下载速度

- 直接输入命令**（切记结尾有斜杠）**

```c++
nvm node_mirror http://npm.taobao.org/mirrors/node/
nvm npm_mirror https://npm.taobao.org/mirrors/npm/
```

- 或者修改nvm安装目录下的setting.txt文件，在文件中加入

```c++
node_mirror: http://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

- mac 和 linux 版 nvm 就没有 node_mirror & npm_mirror 命令 😂 ，设置下载 node 镜像地址的方式是

```shell
export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
```

将等号后面地址换成淘宝镜像([https://npm.taobao.org/mirrors/node](https://npm.taobao.org/mirrors/node/))就可以了 😄 [详见➡️](https://github.com/creationix/nvm#listing-versions)

### 安装node.js

然后输入命令  `nvm install 版本号` （**例如我是要安装10.24.0，所以就输入：**`nvm install 10.24.0` ，如果要安装最新版本使用命令：`nvm install latest` ）安装对应版本的node，会自动安装对应版本的npm。安装完成后可以分别输入命令 `node -v `和 `npm -v` ，检验**node.js**以及对应**npm**是否安装成功，如果可以显示版本号这说明安装成功；

### 切换node版本

- 安装完以后，输入命令 `nvm list`  可以查看你安装的所有**node.js**版本号，以及你当前所选择的node.js运行版本；

- 输入命令 `nvm use 版本号`（**例如：nvm use 10.24.0**）即可选择你本地所使用的Node.js版本，使用此命令行可以根据你自己的需要随意切换node.js版本运行；

### 切换node版本乱码错误

这时，出现了一个问题，当我使用命令切换版本的时候出现了个问题，提示 `exit status 1:一串乱码`，见下图

![Snipaste_2021-09-27_12-34-35](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/9e46d76cf7f45dbd8d243ccef672b3e3.webp)

在网上搜索了一圈，发现都说这个问题是因为nvm安装目录有空格、中文、符号等，重新安装nvm到根目录的纯英文目录就解决了，可我安装的时候就没有这个问题啊（这里要感谢下一直以来自己养成的好习惯，从来不把软件目录设置中文等，毕竟windows本来就是老外开发的啊😂🤣），然后我想会不会是node目录的权限问题，设置了以后还是出错。最后还是在[nvm项目issues](https://github.com/coreybutler/nvm-windows/issues/645#issuecomment-873115432)里发现有人回复说要切换到 `C:\Windows\system32` 再切换版本就OK了，试了一下错误依旧。这时我灵光一闪，会不会还是权限的问题？然后用管理员身份打开cmd.exe，再次输入 `nvm use 10.24.0` ，这时终于显示切换成功了（见下图）。

![Snipaste_2021-09-27_19-06-20](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/92c546d301d85e474f08dda0668559e6.webp)

这里切记，安装新版本的node以后，要重新全局安装npm `npm install npm -g` ，当然记得设置淘宝镜像啊。

```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
// 有时候这样仍然会失败，镜像并没有改变，可使用下面这条命令修改
npm config set registry=http://registry.npm.taobao.org
```

### 卸载node

如果想删除某**node.js**版本的话，输入命令行 `nvm uninstall 版本号`（例如：nvm uninstall 10.24.0）即可删除对应版本。

## 后记

至此，nvm的安装和配置就全部完成了，使用nvm来安装管理node版本以后就方便多了，省去不少麻烦。最后说下虽然node降级成功了，但是安装PicGo的水印插件并没有成功，如果各位大佬谁有解决方案可以留言交流啊。