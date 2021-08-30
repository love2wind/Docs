# 宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行



有的人可能对Go语言很感兴趣，这也是近几年很火的一门编程语言，我们可以在[宝塔面板](https://www.daniao.org/tag/宝塔面板/)Linux环境下安装Go语言环境。

安装环境：CentOS Linux 7.6、[宝塔面板](https://www.daniao.org/tag/宝塔面板/)6.9.3、golang：[go1.12.5.linux-amd64.tar.gz](https://dl.google.com/go/go1.12.5.linux-amd64.tar.gz)

这篇文章就来水一下如何在宝塔面板Linux环境下安装Go语言环境和程序的如何运行。

#### 更新下简便的安装方法：

**1）安装go语言**

宝塔面板安装go语言，方法如下：（如果有更新版本自己修改版本号~）

```
wget https://golang.org/dl/go1.15.2.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.15.2.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' > /etc/profile.d/golang.shsource /etc/profile.d/golang.sh
```

**2）安装好之后，可以用如下命令检查是否安装成功~**

```
go versiongo version go1.15.2 linux/amd64
```

#### 一：简介

下载之前先去官网溜达下，点击【download go】就可进入下载页面：

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-1-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-1-min.png)

官网：https://golang.google.cn/

下载：https://dl.google.com/go/go1.12.5.linux-amd64.tar.gz

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-2-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-2-min.png)

根据自己的系统环境下载相应的版本，大鸟这里选择的是go1.12.5.linux-amd64.tar.gz。

#### 二：下载安装

宝塔面板可以直接在面板里面下载安装，大鸟这里为了方便，直接就在命令环境下面下载安装配置了。

*2.1下载*

SSH工具连接服务器开始操作：

```
cd /www/server && wget -O golang.tar.gz https://dl.google.com/go/go1.12.5.linux-amd64.tar.gz
```

这些可以直接在面板环境里操作，也很方便。

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-3-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-3-min.png)

*2.2解压*

下载好之后解压：

```
tar -xzvf golang.tar.gz
```

*2.3添加环境变量*

添加环境变量，使用vim 打开/etc/profile 文件。

```
vim /etc/profile
```

在profile 最底部添加：

```
export GOROOT=/www/server/go
export GOBIN=$GOROOT/bin
export GOPKG=$GOROOT/pkg/tool/linux_amd64
export GOARCH=amd64
export GOOS=linux
export GOPATH=/www/wwwroot/Golang
export PATH=$PATH:$GOBIN:$GOPKG:$GOPATH/bin
```

丢一张图：

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-4-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-4-min.png)

添加好之后，保存退出，然后执行如下命令使其生效：

```
source /etc/profile
```

*2.4测试是否生效*

使用如下命令来测试Go语言环境是否安装成功。

```
go version
```

丢一张图：

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-5-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-5-min.png)

图上所示，我们已经安装成功了。

#### 三：创建GOROOT目录

使用如下命令来创建，不过我们可以用面板环境来可视化操作：

```
mkdir /www/wwwroot/Golang
```

丢一张图看看：

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-6-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-6-min.png)

以上就完全安装好go了，因为是宝塔面板的环境以上所以操作都可直接在面板里操作。

#### 四：go run

我们可以测试一段代码来验证go语言的运行。我们到Golang里面新建一个文件命名为test.go

```
touch test.go
```

之后用vi简单编辑下，也可以直接到宝塔面板里新建编辑：

```
vi test.go
```

复制一段代码进去：

```
package main import "fmt" func main() {   /* 这是我的第一个简单的程序 */   fmt.Println("Hello, 大鸟博客!")}
```

丢一张图看看：

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-7-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-7-min.png)

代码保存好之后，我们执行 Go 程序，如何执行呢，打开命令行，并进入程序文件保存的目录中。

```
 go run test.go
```

我们看图：

[![宝塔面板Linux环境-安装Golang:Go语言环境安装以及程序如何运行](https://www.daniao.org/wp-content/uploads/2019/05/golang-8-min.png)](https://www.daniao.org/wp-content/uploads/2019/05/golang-8-min.png)

成功执行了这一段代码，输出了“hello，大鸟博客！”

#### 五：总结

整个环境的安装和简单的测试运行代码就说完了，希望对想学习Go语言的同学能有一点帮助。

Go 是一个开源的编程语言，它能让构造简单、可靠且高效的软件变得容易。

Go是从2007年末由Robert Griesemer, Rob Pike, Ken Thompson主持开发，后来还加入了Ian Lance Taylor, Russ Cox等人，并最终于2009年11月开源，在2012年早些时候发布了Go 1稳定版本。现在Go的开发已经是完全开放的，并且拥有一个活跃的社区。

Go 语言特色



- 简洁、快速、安全
- 并行、有趣、开源
- 内存管理、数组安全、编译迅速



Go 语言用途



1. Go 语言被设计成一门应用于搭载 Web 服务器，存储集群或类似用途的巨型中央服务器的系统编程语言。
2. 对于高性能分布式系统领域而言，Go 语言无疑比大多数其它语言有着更高的开发效率。它提供了海量并行的支持，这对于游戏服务端的开发而言是再好不过了。