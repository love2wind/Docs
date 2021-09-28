## 前言

写这篇文章的起因是，家里电脑重新安装系统后，在搭建环境的过程中Node.js安装出现错误，公司电脑上当时没有问题啊，大概率是环境变量设置的问题，Google之后发现是在设置环境变量的时候输入错误导致的缓存问题，这个留到后面说。重新安装一遍，顺便记录一下安装过程，以备后用。

## 一、什么是Node.js？

简单的说 Node.js 就是运行在服务端的 JavaScript。Node.js是一个基于 Chrome V8 引擎的 JavaScript 运行环境；Node.js使用一个事件驱动、非阻塞式 I/O 的模型，使其轻量且高效；Node.js的软件包生态系统 [**npm**](https://www.npmjs.com/) 是全球最大的开源库生态系统。

> **官方网站：** https://nodejs.org
>
> **Node.js中文网：** http://nodejs.cn

## 二、如何安装

!> **本机测试环境：**Windows 10 企业版 LTSC  64bit

#### 1.下载安装包

前往Node.js 官方网站下载自己系统对应的版本：[**戳这里前往官方网站下载**](https://nodejs.org/en/download/)

这里要说明一下，官网有两个版本下载，一个LTS（long support stable）版本，也就是长期稳定版，也是官方推荐的版本；另一个是Current版本，也就是最新版，一般情况下这个版本会支持更多新功能及新特性，但是可能会不太稳定，容易出现各种错误，非高级开发用户不推荐大家下载。相信能来看这篇文章的同学都会去下载LTS版😂

![image-20210812003026527](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/ccc392497b3cff5d7091d3fadfb6eb74.webp)

 

这里，我选择64位稳定版的windows系统安装包，下载完成，安装包如下：

![image-20210812003930974](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/d76e46ef4a3b4759ba4c810124c2c3db.webp)

####  2.安装

双击安装包进行安装，和其他软件安装一样，如下图所示，基本是一路下一步，只到看见`Finish`就算安装完成了。

**需要说明的是**，安装路径这里推荐大家**安装到非系统盘**，我的安装路径为`“D:\nodejs”`

![image-20210812012936794](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/57d9414a851142dcbd1069f5906921b1.webp)

####  3.验证

安装成功后，我们来测试一下安装是否成功呢？快捷键`WIN+R`调出运行窗口，输入`cmd`，输入`node -v` 和 `npm -v` ，如下图所示，如果能看到node和npm的版本号，说明你已经安装成功了。

- `node -v`：显示安装的nodejs版本
- `npm -v`：显示安装的npm版本

![image-20210812014909115](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/d2060871b075b04095baf75b441c9ca5.webp)

 安装完成后，npm随安装程序自动安装，作用就是对Node.js依赖的包进行管理，我的npm安装路径就在`D:\nodejs\node_modules`。

#### 3.修改全局模块路径和缓存路径

!>  🔔 这一步骤可选，大家自行选择是否修改。

如果这里不修改，我们在执行一些全局安装命令的时候，系统会默认将模块安装和缓存在`C:\Users\用户名\AppData\Roaming`路径下的`npm`目录（**注意：此文件夹默认是隐藏的，需要设置显示隐藏的文件夹，在"查看"菜单中设置**）和`npm_cache`目录中，随着安装的模块越来越多，对系统盘的占用还是很大的，这也就是我们前面提到的为什么推荐将node.js安装在非系统盘了。不方便管理且占用C盘空间，

所以我们要重新配置自定义的全局模块安装目录，将他们放在node.js的安装目录下。

在`D:\nodejs\`目录下新建两个文件夹 `node_global` 和 `node_cache`，再在`node_global`文件夹下新建一个`node_modules`文件夹，用以配置环境变量。此时，还没有更改完成，需要手动指定到这两个文件夹中。

**第一种方法：**

`win+R`打开运行窗口，输入`cmd`，再输入以下两条指令

```shell
npm config set prefix "D:\nodejs\node_global"
npm config set cache "D:\nodejs\node_cache"
```

注意这里要把命令中的`D:\nodejs\node_global`和`D:\nodejs\node_cache`分别改为你对应的路径。

**第二种方法：**

在nodejs的安装目录下，进入node_modules—>npm—>npmrc文件，打开编辑，添加以下参数：

```shell
prefix=D:\nodejs\node_global
cache=D:\nodejs\node_cache
```

#### 4.配置镜像站

由于npm官方网站在国外，所以我们从官方拉取模块的时候速度不怎么友好，所以这里要将拉取站点修改成淘宝的镜像站以提升速度。

和上面配置全局路径一样，我们可以直接用命令

````shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
// 有时候这样仍然会失败，镜像并没有改变，可使用下面这条命令修改
npm config set registry=http://registry.npm.taobao.org
````

或者修改npmrc文件，添加参数

````shell
registry=http://registry.npm.taobao.org
````

设置完可以用命令`npm config list` 查看配置参数

#### 5.设置环境变量

上面的步骤执行完后，我们还差最后一步，设置环境变量了。

> 桌面右键点击**此电脑**—>**高级系统设置**—>**环境变量**

- 在**系统变量**中，新建一个变量，变量名为 `NODE_PATH`， 值为`D:\nodejs\node_global\node_modules`

- 修改**用户变量**中的`Path`变量，编辑用户变量里的**Path**，将默认的npm的路径`C:\Users\用户名\AppData\Roaming\npm`改为：`D:\nodejs\node_global`

![image-20210812030534423](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/3939267778500533b6d49a0fd7669640.webp)

#### 重新全局安装npm

因为我们改变了，全局目录，所以在这里使用如下命令重新全局安装下npm

```shell
npm install npm -g
```

## 常见问题

### 升级

#### 1）升级npm的版本

 使用命令：`npm install -g npm`

```kotlin
npm install -g npm  或者 npm install npm -g    /*升级到最新版本*/
npm install npm@latest -g    /*升级到最新版本*/
npm install npm@4.1.2 -g    /*升级到指定版本*/
```

#### 2）升级node的版本

去node官网，下载新版本node的 msi 安装包，然后覆盖安装之前的版本来完成更新操作。

我们在覆盖的时候要检查之前安装 node 的路径，使用命令 `where node` 查看node的安装路径，注意安装路径选择为和之前一样的路径。
**安装 node 会同步更新 npm 的版本号，选择了最新的 node 版本，那么 npm 也会更新到最新的版本。**

#### 3）踩坑警告

关于Windows升级node，流传着使用`npm install -g n --force`的方法，安装 n 模块，node版本管理工具。
 安装n模块：`npm install -g n`，执行后会报错
 尝试使用强制安装命令：`npm install -g n --force`，看上去似乎成功了，以为可以愉快地使用命令`n stable`更新node稳定版本了，却提示找不到命令。

force之后输入`n stable` 后提示错误，不是内部命令， 其实通过之前的报错提示，也可以略见一斑，提示win32操作系统不支持：

```kotlin
Unsupported platform for n@2.1.4: 
wanted: {"os":"!win32","arch":"any"}
current: {"os":"win32","arch":"x64"}
```

搜了一下[n模块官方](https://www.npmjs.com/package/n)提示： `Note: n is not supported natively on Windows.` Windows自然情况下是不支持n模块的。 所以出现了上面虽然强制安装了，但是并不支持使用的情况。

### 降级

#### 1）卸载原有版本node

进入 `控制面板` 将node.js卸载，然后将node.exe所在的父目录里面的所有东西都删除，如果不记得了，用 `where node` 命令查看。

#### 2）安装nvm管理工具

?> [点击这里查看nvm完整安装设置教程](/note/site/nvm)

先关掉杀毒软件，不然会弹出警告！然后从官网下载最新安装包 https://github.com/coreybutler/nvm-windows/releases，解压得到 `nvm-setup.exe`

**a. 运行此文件进行安装**

- 勾选 **`I accept the agreement`** 点击 `Next`；
- 选择**nvm**安装路径，点击 `Next`；
- 选择**node**安装路径，点击 `Next`；
- 点击 `Install` 安装；
- 命令行用 `nvm` 验证。

**b. 安装node.js版本**

- 输入命令行 `nvm list available` 查看可用的node.js版本号；
- 输入命令行 `nvm install 版本号`(例如：nvm install 12.17.0)即可安装对应版本以及自动安装对应的npm版本。除了上面显示的node.js版本，其他版本号也可以下载，只不过有些可以准确下载，有些会出现npm版本不会自动下载；
- 安装完成后可以分别输入命令行 `node -v `和 `npm -v` ，检验**node.js**以及对应**npm**是否安装成功，如果可以显示版本号这说明安装成功；
- 输入命令行 `nvm use 版本号`（例如：nvm use 12.17.0）即可选择你本地所使用的Node.js版本，使用此命令行可以根据你自己的需要随意切换node.js版本运行；
- 输入命令行 `nvm list` 查看你安装的所有**node.js**版本号，以及你当前所选择的node.js运行版本；
- 如果想删除某**node.js**版本的话，输入命令行 `nvm uninstall 版本号`（例如：nvm use 12.17.0）即可删除对应版本。
- 设置nvm镜像，提高下载速度。**切记结尾有斜杠

```c++
nvm node_mirror http://npm.taobao.org/mirrors/node/
nvm npm_mirror https://npm.taobao.org/mirrors/npm/
```

- 或者修改nvm安装目录下的setting.txt文件，在文件中加入

```c++
node_mirror: http://npm.taobao.org/mirrors/node/npm_mirror: https://npm.taobao.org/mirrors/npm/
```

mac 和 linux 版 nvm 就没有 node_mirror & npm_mirror 命令 😂 ，设置下载 node 镜像地址的方式是

```
export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
```

将等号后面地址换成淘宝镜像([https://npm.taobao.org/mirrors/node](https://npm.taobao.org/mirrors/node/))就可以了 😄 [详见➡️](https://github.com/creationix/nvm#listing-versions)

>>>>>>> 288ee7c5e17b2e2e128bcabe0f44ce456c12d006

### 缓存问题

这里就说下前面提到的安装错误，如下图的错误码，这就是**缓存的问题，清下缓存就解决了**。

<img src="https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/9dba80f02b2c998b7f717f8618bcd0ab.webp" style="zoom:67%;" />



**解决方法：**

- **方法一：**删除`C:\Users\{账户}\.npmrc`文件，切记不是nodejs安装目录npm模块下的那个npmrc文件。
- **方法二：**控制台输入：`npm cache clean --force`

### 安装中用的几个常用命令

```shell
#查看配置
npm config list
#查看镜像服务器
npm config get registry
#查看能否获取镜像服务器中的模块信息，下面的就是要查看的模块名称
npm info vue
#清理缓存
npm cache clean --force
#查看全局模块目录里有什么模块
npm list -global
```

## 后记

到这里node.js的安装就算彻底完成了，本地测试没有问题，如果你有什么问题可以再按照上面的流程仔细核对一遍，应该就能解决了。

你可以按照 [这篇文章](https://docs.love2wind.com/#/note/site/docsify) 快速上手安装一个docsify进行测试。

如果在安装配置过程中还有不明白的地方，欢迎在本站留言交流！



## 附录

### 网上几个常见报错及解决方案

>  转载自：`https://juejin.cn/post/6844903824038051848`

#### 1. npm ERR! code ELIFECYCLE npm ERR! errno 1

```
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! phantomjs-prebuilt@2.1.15 install: `node install.js`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the phantomjs-prebuilt@2.1.15 install script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
```

#### 解决方案

```
npm install --save-dev node-sass
```

#### 2. npm run dev error [npm ERR! code ELIFECYCLE]

```
Laravel Mix Version: 1.4.3 
Node Version: v8.9.1 
NPM Version: 5.5.1 
OS: macOS 10.12.6

Description: 
ze Chunks Chunk Names 
mix.js 8.27 kB 0 [emitted] mix 
npm ERR! code ELIFECYCLE 
npm ERR! errno 2 
npm ERR! @ development: cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js 
npm ERR! Exit status 2 
npm ERR! 
npm ERR! Failed at the @ development script. 
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in: 
npm ERR! /Users/sunny/.npm/_logs/2017-12-21T17_00_33_319Z-debug.log 
npm ERR! code ELIFECYCLE 
npm ERR! errno 2 
npm ERR! @ dev: npm run development 
npm ERR! Exit status 2 
npm ERR! 
npm ERR! Failed at the @ dev script. 
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in: 
npm ERR! /Users/sunny/.npm/_logs/2017-12-21T17_00_33_347Z-debug.log
```

**node_modules安装问题，执行以下：**

```
rm -rf node_modules
rm package-lock.json
npm cache clear --force
npm install
```

这一步清除npm缓存很重要

```
npm cache clear --force
```

#### 3. npm install时,报错 install: `node install.js`安装失败

```
 error chromedriver@2.33.2 install: `node install.js`
 error Exit status 1
 error Failed at the chromedriver@2.33.2 install script.
 error This is probably not a problem with npm. There is likely additional logging output above.
```

初步判断是这个zip文件没下载下来，然后手动下载一个`chromedriver_win32.zip`丢到`C:\Users\用户\AppData\Local\Temp\chromedriver\`目录下，结果因为这是一个临时文件夹，每次初始化的时候都会重新下载这个文件，从而又无法初始化。

**解决方案 ：**

1. **加参数**

```
  npm install --ignore-scripts
```

  --ignore-scripts表示npm将不会运行在package.json中指定的scripts脚本

**2. 更换数据源**

```shell
npm install chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
```

### 参考文献

windows系统node升级：https://www.jianshu.com/p/0f3fdf6c0d5f

windows如何把已安装的nodejs高版本降级为低版本(图文教程)：https://www.jb51.net/article/202124.htm

nvm 设置下载 node 的镜像地址 ：https://github.com/xhlwill/blog/issues/7

