## 前言

写这篇文章的起因是，家里电脑重新安装系统后，在搭建环境的过程中Node.js安装出现错误，公司电脑上当时没有问题啊，大概率是环境变量设置的问题，Google之后发现是在设置环境变量的时候输入错误导致的问题，果断卸载，然后重新安装，最后在这里记录一下，以备后用。

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

![image-20210812003026527](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/202108120308598.png)

 

这里，我选择64位稳定版的windows系统安装包，下载完成，安装包如下：

![image-20210812003930974](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/202108120308130.png)

####  2.安装

双击安装包进行安装，和其他软件安装一样，如下图所示，基本是一路下一步，只到看见`Finish`就算安装完成了。

**需要说明的是**，安装路径这里推荐大家**安装到非系统盘**，我的安装路径为`“D:\nodejs”`

![image-20210812012936794](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/202108120308976.png)

####  3.验证

安装成功后，我们来测试一下安装是否成功呢？快捷键`WIN+R`调出运行窗口，输入`cmd`，输入`node -v` 和 `npm -v` ，如下图所示，如果能看到node和npm的版本号，说明你已经安装成功了。

- `node -v`：显示安装的nodejs版本
- `npm -v`：显示安装的npm版本

![image-20210812014909115](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/202108120308710.png)

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

`npm config set registry=http://registry.npm.taobao.org`

或者修改npmrc文件，添加参数

`registry=http://registry.npm.taobao.org`

#### 5.设置环境变量

上面的步骤执行完后，我们还差最后一步，设置环境变量了。

> 桌面右键点击**此电脑**—>**高级系统设置**—>**环境变量**

- 在**系统变量**中，新建一个变量，变量名为 `NODE_PATH`， 值为`D:\nodejs\node_global\node_modules`

- 修改**用户变量**中的`Path`变量，编辑用户变量里的**Path**，将默认的npm的路径`C:\Users\用户名\AppData\Roaming\npm`改为：`D:\nodejs\node_global`

![image-20210812030534423](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/202108120308356.png)

##  后记

到这里node.js的安装就算彻底完成了，本地测试没有问题，如果你有什么问题可以再按照上面的流程仔细核对一遍，应该就能解决了。

你可以按照 [这篇文章](https://docs.love2wind.com/#/note/site/docsify) 快速上手安装一个docsify进行测试。

如果在安装配置过程中还有不明白的地方，欢迎在本站留言交流！
