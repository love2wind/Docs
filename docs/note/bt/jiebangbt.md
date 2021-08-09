## 安装aapanel

我们可以安装宝塔国际版aapanel，和宝塔面板使用起来没有任何区别，只不过aapanel是英文版本。

https://www.aapanel.com/reference.html

#### Installation

Centos Installation

```
yum install -y wget && wget -O install.sh http://www.aapanel.com/script/install_6.0_en.sh && bash install.sh
```

Ubuntu/Deepin Installation

```
wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && sudo bash install.sh
```

Debian Installation

```
wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && bash install.sh
```

Fedora Installation

```
yum install -y wget && wget -O install.sh http://www.aapanel.com/script/install_6.0_en.sh && bash install.sh
```

## 2、安装宝塔旧版本

**1）可以使用宝塔5.9**

官网的安装命令：https://www.bt.cn/bbs/thread-1186-1-1.html

**2）安装宝塔历史版本：**

目前最新版本是7.6

```
http://download.bt.cn/install/update/LinuxPanel-5.9.1.zip（目前仍然很多人在用的版本）http://download.bt.cn/install/update/LinuxPanel-7.0.1.zip
http://download.bt.cn/install/update/LinuxPanel-7.0.2.zip
http://download.bt.cn/install/update/LinuxPanel-7.0.3.zip
http://download.bt.cn/install/update/LinuxPanel-7.1.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.1.1.zip
http://download.bt.cn/install/update/LinuxPanel-7.2.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.3.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.2.zip （有pma漏洞）http://download.bt.cn/install/update/LinuxPanel-7.4.3.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.5.zip（会有绑定提醒）http://download.bt.cn/install/update/LinuxPanel-7.4.6.zip
```

**3）百度网盘收藏了。如果上面失效，可以来这里下载**

链接: https://pan.baidu.com/s/1a2b9Bt9_j9sm6DCUESpycw 提取码: dkcm

**4)  官方给出的手动升级方法**

```
1、下载离线升级包
2、将升级包上传到服务器中的/root目录
3、解压文件：unzip LinuxPanel-*
4、切换到升级包目录： cd panel
5、执行升级脚本：bash update.sh
6、删除升级包：cd .. && rm -f LinuxPanel-*.zip && rm -rf panel
```

**5)  简单设置下**

为了更安全，你可以执行以下内容，避免一些问题~~

```
echo '127.0.0.1 bt.cn' >>/etc/hosts
```

## 取消强制登录

上面的方法可能都不是你喜欢的，这里介绍写其他的。如果以后遇到问题会更新在这里。

**1）目前还能用的方法删除**

```
 cp /www/server/panel/data/bind.pl /www/server/panel/data/binds.pl  #防止出问题先备份这个文件
 rm -f /www/server/panel/data/bind.pl   #接着删除文件
```

删除后，刷新浏览器问题解决。

**2）如果你的出问题了，那么只需要恢复即可。**

```
cp /www/server/panel/data/binds.pl /www/server/panel/data/bind.pl  #恢复文件
```

**3）脚本，直接运行即可。**

```
echo "{\"uid\":1000,\"username\":\"admin\",\"serverid\":1}" > /www/server/panel/data/userInfo.json
```

运行后，刷新浏览器问题解决。

### 5、修改__init__.py

通过禁用/www/server/panel/BTPanel/__init__.py文件的某些代码来禁止绑定。我们通过路径找到__init__.py文件，这个如何找这个文件，可以用SFTP来连接到服务器，然后通过路径找到这个文件。拖到桌面用编辑器打开，比如说，sublime，editplus等等。

**1）181-182行的代码注释掉，前面加#即可，如下。**

```
 #if not public.is_bind():#return redirect('/bind',302)
```

**2）230-231行注释掉，如下：**

```
 #if not os.path.exists('data/userInfo.json'):#data['bind'] = os.path.exists('data/bind.pl')
```

**3）ssh连接到服务器，输入bt命令，接着输入9，清除面板缓存即可。**