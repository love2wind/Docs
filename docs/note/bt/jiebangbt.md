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

## 宝塔面板破解付费插件

打开`/www/server/panel/class`找到`panelplugin.py`这个文件 。（宝塔会自动更改文件，建议关闭宝塔被此文件的写入功能）

在文件中`搜索`以下代码

```
softList['list'] = tmpList
```

在这段代码**下面加入**以下代码

```
#专业版破解
softList['pro'] = 1
        for soft in softList['list']:
            soft['endtime'] = 0
#企业版破解
softList['ltd'] = 99999999999
        for soft in softList['list']:
            soft['endtime'] = 0
```

PS ：

*安装后，你的宝塔界面**可能不会**显示宝塔**专业版**或者**企业版**图标，但**实际**上你**已经获得**特权！但如果你想**获得特权图标**，请查看网站**右侧目录栏**，**单击图标修改**。如果您安装**网站监控报表**插件后**不能直接使用**， 我会单列一个目录介绍 **开启方法**，请点击右侧**目录**栏>**开启网站监控报表***

## 开启网站监控报表

**安装**网站监控报表后

打开`/www/server/panel/plugin/total/`中的 `total_main.py`

1. 旧版统计插件破解方法

   在文件中搜索以下代码

   ```
   if 'bt_total' in session: return public.returnMsg(True,'OK!');
   ```

在这段代码下面加入以下代码

```
session['bt_total'] = True
return public.returnMsg(True,'OK!');
```

如果搜索不到此段代码，则说明你是新版统计插件

1. 新版统计插件破解方法

   在文件中搜索以下代码（大概位置在255-265行之间）

   ```
   if cache.get('bt_total'): return public.returnMsg(True, 'OK!');
   ```

在这段代码下面加入以下代码

```
cache.set('bt_total', True)
return public.returnMsg(True,'OK!');
```

[![请输入图片描述](https://pic.rmb.bdstatic.com/bjh/e84d102bd8105230b8af1cf1ed3ea8ab.png)](https://pic.rmb.bdstatic.com/bjh/e84d102bd8105230b8af1cf1ed3ea8ab.png)

[请输入图片描述](https://pic.rmb.bdstatic.com/bjh/e84d102bd8105230b8af1cf1ed3ea8ab.png)



至此，网站监控报表破解成功，重启面板即可体验!

## 图标修改

这个功能没有太大的用处，纯属装13的，感兴趣的可以试试

找到`/www/server/panel/data`目录，编辑`plugin.json`文件

搜索`"recommend"`，找到前面的`pro`和`ltd`

[![plugin.json](https://pic.rmb.bdstatic.com/bjh/bb3f6c00acc649ad4d2652c16cdd02d2.png)](https://pic.rmb.bdstatic.com/bjh/bb3f6c00acc649ad4d2652c16cdd02d2.png)

[plugin.json](https://pic.rmb.bdstatic.com/bjh/bb3f6c00acc649ad4d2652c16cdd02d2.png)



其中**pro**表示是**专业版**，**ltd**表示是**企业版**

**pro**和**ltd冒号后**的**数字**

**-1**表示**无**

**pro**为**0**时为**专业版永久授权**，企业版**同理**

**数字**请填写**时间戳**([时间戳(Unix timestamp)转换工具 - 在线工具 (tool.lu)](https://tool.lu/timestamp/)

[![专业版图标](https://pic.rmb.bdstatic.com/bjh/d96609efeb27d4108d75a670350d7caf.png)](https://pic.rmb.bdstatic.com/bjh/d96609efeb27d4108d75a670350d7caf.png)

[专业版图标](https://pic.rmb.bdstatic.com/bjh/d96609efeb27d4108d75a670350d7caf.png)



[![企业版图标](https://pic.rmb.bdstatic.com/bjh/07f22131cf30fc287599fd396a22bed0.png)](https://pic.rmb.bdstatic.com/bjh/07f22131cf30fc287599fd396a22bed0.png)

[企业版图标](https://pic.rmb.bdstatic.com/bjh/07f22131cf30fc287599fd396a22bed0.png)



## 后语

如果你需要宝塔面板插件，可从此处下载

([Pandora's Box (chinft.com)](http://file.chinft.com/宝塔面板))(来自chinft.com)