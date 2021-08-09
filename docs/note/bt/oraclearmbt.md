甲骨文新推出的ARM架构的免费云主机实际最高可以拥有4核心24G内存4G带宽200G存储的实例。但是CPU是ARM架构，所以在实际使用中安装BT宝塔面板时遇到了一些问题导致无法完成安装，实际都是关联软件的原因。这里搬主题就分享一下ARM架构安装BT宝塔面板及NGINX+PHP+MySQL的安装教程。

## 一、手动安装

很多人会通过DD的方式安装Debian，但是这是存在风险的，很多人被甲骨文删号的原因是被系统侦测到闲置，而DD系统会导致部分检测功能失效，所以并不推荐这样做，以下为默认的ubuntu下进行安装。

首先更新系统软件包：

```
apt-get update
```

先正常安装宝塔！

```
curl -sSO http://download.bt.cn/install/install_panel.sh && bash install_panel.sh
```

然后安装各项依赖：

**以下是以Nginx ，PHP8.0， Mysql 5.7为例**

```
apt-get install gcc build-essential
apt-get install gcc gcc-c++ autoconf automake
apt-get -y install zlib zlib-devel openssl openssl-devel pcre pcre-devel
```

下载Libiconv

```
wget http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.13.1.tar.gz
tar zxvf libiconv-1.13.1.tar.gz
cd libiconv-1.13.1
```

配置libiconv

```
./configure -prefix=/usr/local --build arm-pc-linux
```

编译安装

```
make
make install
```

创建文件链接到Libiconv库

```
ln -s /usr/local/lib/libiconv.so /usr/lib
ln -s /usr/local/lib/libiconv.so.2 /usr/lib/libiconv.so.2
```

安装完成后再宝塔面板内完成对WEB环境的配置即可。

最后顺手开启BBR：

```
wget -N --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && bash bbr.sh
```

检查一下是否开启成功以及是否自启动：

```
sysctl net.ipv4.tcp_available_congestion_control
sysctl net.ipv4.tcp_congestion_control
sysctl net.core.default_qdisc
lsmod | grep bbr
ps -ef | grep bbr
```

## 二、适配ARM架构的开心版安装

全新安装：默认安装的是 7.5.1 面板，请在面板上点击 “更新” 或者 “修复” 升级到最新版，或者执行下面的 “Linux面板7.5.2升级命令”

已安装（免费版）：直接执行下面的 “Linux面板7.5.2升级命令”

甲骨文arm架构的面板 nginx是专属订制的“Nginx openresty.1.19.3.1” btwaf防火墙、系统防火墙、监控报表 完美使用，其他功能一切正常！

甲骨文arm架构的面板 apache是使用的官方的 apache防火墙“xxx”功能使用不了， 监控报表使用不了，其他功能一切正常！ >>>> 这里推荐使用 nginx环境

移除了一些 不兼容arm架构的环境与插件，宝塔没适配arm架构 而官方适配arm架构的环境，会根据大家需求为大家适配上架！

> **更新记录**
>
> - 修复了安装面板需要手动放行的问题！
> - 修复了面板上放行端口需要手动放行的问题！
> - 修复了面板修改端口需要手动放行的问题！
> - 修复了 btwaf防火墙、系统防火墙、监控报表 无法使用的问题！
> - 已知apache环境下 apache防火墙 监控报表等问题无法使用，推荐使用 nignx环境 后期会修复！
>

**目前仅支持企业版**
已在 **甲骨文 Red Hat Enterprise Server 7.9 / Ubuntu 20.04.2 LTS** 测试 暂未发现BUG！

```
curl -sSO https://download.seele.wang/ltd/install/arm/install_panel.sh && bash install_panel.sh
```

Linux面板7.5.2升级企业版命令：

```
wget -O updatearm.sh https://download.seele.wang/ltd/install/arm/updatearm.sh && bash updatearm.sh
```