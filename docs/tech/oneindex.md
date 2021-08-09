[![主图](https://tva1.sinaimg.cn/mw690/0084aYsLly1gcnli3fk8yj30go0cdq3y.jpg)](https://tva1.sinaimg.cn/mw690/0084aYsLly1gcnli3fk8yj30go0cdq3y.jpg)

OneIndex是映射Onedrive网盘的一个开源程序。可以将Onedrive存储的文件展示，直链下载。**视频、音乐等媒体还能在线播放**！不用服务器空间，不走服务器的流量！几乎零成本搭建自己的专属网盘。

## 准备工作

1）一台支持PHP的虚机 or VPS or 云服务器等等

2）准备一个OneDrive账号，微软账号自带15G，准备好稍后登陆用

3）(可选)准备一个域名用于解析

## 下载OneIndex

[btnblue href="https://github.com/zwying0814/oneindex" target="blank"]点我跳转GitHub[/btnblue]

## 安装步骤

首先，新建一个网站(注意：OneIndex不需要数据库)，将程序上传到网站根目录，解压。

[![上传解压](https://tva2.sinaimg.cn/large/0084aYsLly1gcnkykhfmwj319f0hdabq.jpg)](https://tva2.sinaimg.cn/large/0084aYsLly1gcnkykhfmwj319f0hdabq.jpg)

然后，在浏览器访问相应的网址，进入网页安装

[![安装步骤](https://tva2.sinaimg.cn/large/0084aYsLly1gcnl40fk0wg30qe0nm1ky.gif)](https://tva2.sinaimg.cn/large/0084aYsLly1gcnl40fk0wg30qe0nm1ky.gif)

安装完成后，就可以使用了。

## 文件管理

两种方法：
1、如果电脑里自带OneDrive，那么可以直接在文件资源管理器操作（推荐）
2、通过访问 https://onedrive.live.com/ 来上传

上传完成后，如果没有显示，记得到后台清除缓存

## 题外话

百度搜索`index of / – OneIndex`就能找到网友们搭建的网盘。

网盘存放的东西比较多，有好多小视频，美图等 ![img](https://cdn.jsdelivr.net/gh/zwying0814/Cuteen@4.6/static/emoji/aru/E8A385E5A4A7E6ACBE_2x.png) 营养又跟不上了！

[宝塔面板部署OneIndex教程 - 秦枫鸢梦 (zwying.com)](https://blog.zwying.com/archives/29.html)



> **OneIndex 是一款针对大微软巨无霸 Onedrive 网盘的开源程序。他能够将在Onedrive 中的文件用目录形式展示出来，用户可以通过连接直接下载。甚至视频文件还可以在线播放！对于用大量空间需求的用户可以不用服务器空间，不用耗费服务器的流量！**

> **Oneindex的优点：**
>
> - **响应式，支持小屏设备**
> - **视频、音乐在线播放**
> - **图片在线预览**
> - **代码在线查看**
> - **支持文件夹加密**
> - **支持自定义头部、底部显示**
> - **支持文件上传**
>
> **基于以上优点，所以推荐给大家，搭建自己的私人网盘！以后下载资源再也不用受××网盘的速度限制啦！**

------

## 搭建Oneindex准备工作

- **宝塔面板最新版本，lnmp环境自行配置好**
- **PHP空间，PHP 5.6+ 需打开curl支持**
- **OneDrive 账号 (个人、企业版或教育版/工作或学校帐户)**
- **OneIndex 程序**
- **一个域名和VPS(或虚拟主机)**

> **提示：近段时间Onedrive作者不知何原因已经删库了，在作者的github上已经找不到了，不过我们可以用网友们fork下来的Oneindex程序。**
> **下载地址：https://dl.cyz4531.top/?/e%E3%80%81%E6%BA%90%E7%A0%81/oneindex%E6%BA%90%E7%A0%81/oneindex.zip**

------

## 宝塔安装Ondindex

> **步骤一：添加站点 -> 上传Oneindex程序 -> 程序压缩包解压**

**如图：**
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDI1Y2E0MTc5ZGY1MTQwZmY4NzRjMWQxYzRlMzc3ZDg5cS5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSGI2Y2U0MWVjY2FjNzQ5NDJiMThhODIyYjc3NmU4MTgwaC5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDEwMjgwNjZhODU5MjRkYTA4ZTI4ZGVmYmI2Y2UwNzZlaS5qcGc?x-oss-process=image/format,png#pic_center)

------

> **步骤二：网站设置SSL -> 点击网站的设置 -> SSL -> 申请免费的ssl证书 -> 强制HTTPS**

**如图：**
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSGZjNzlkYmVmZDBmMTRhYjRiZWM5OTUwYTU3OGUzNWY0eC5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDU0MTlkNzMwYzcwNjQ3NmNhZDg1ZjI1ODE5NzIwZTY4by5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSGJkNDJiMTk1ZWQ1NzQ2NWE5ZWIxYWE0ZTQ0MmYzNzNjMi5qcGc?x-oss-process=image/format,png#pic_center)

------

> **步骤三：登陆域名，进入到Oneindex的安装程 -> 复制粘贴应用机密和应用ID -> 绑定OneDrive账号即可**

**如图：**
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSGMxYjJhYmQ0ZTE0MjRlNDBiZjBlOWFkNWQwYzdlY2U5TS5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDZhN2Y4NDAyMzAxNDRhZDZhNzUwMGU1MjQ3NmI1YmVjdS5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDU2MzNmNjU3NTdhODRkN2ViNTFiMGFhNDI1NWEyNGZjbC5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDNhNWFhNzEwMjM5ZTRlMTU4YjE3Yzk5Y2NhNjQyN2Q1OC5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDQ4YzViOWZhMjQ1MDRmZTdhNTY2MWE4YzQyYTQyMWM4OC5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDU4NjUzMmUzN2QzYTRlNDk4MWE4YTAyZDhiNzc1Y2MxdC5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDE5OGZlM2I2YzI2ZjQxYmFiYTEwNDdhNzEzNzViNjI5Yi5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDU2YWUwZTY1MWM0ZTQ3ZTRhN2YxYmVjMzA2ZTlkZTc3Wi5qcGc?x-oss-process=image/format,png#pic_center)

> **提示：后台的初始密码 oneindex ,记得修改密码**

------

## 宝塔设置定时任务

> **为了提高提高系统访问性能，我们需要定时刷新缓存，不然你存取的文件有的时候看不到，影响体验。我们可以直接用宝塔面板自带的定时任务来设置，分别是每小时刷新一次token 和 每十分钟后台刷新一遍缓存。**

**步骤一：宝塔计划任务**

任务类型：Shell脚本 

任务名：每小时刷新一次token 

执行周期：每小时 0分钟 

脚本内容：php `你的网站目录路径`/one.php token:refresh 

**步骤二：**

任务类型：Shell脚本 

任务名：每十分钟后台刷新一遍缓存 

执行周期：N分钟 10分钟 

脚本内容：php `你的网站目录路径`/one.php cache:refresh   

**如图：**
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSGM3Y2YzY2IxNWQ2MjRiMzFhZWZmMTc4ZjlmYzI3YmYwSi5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSDU3Y2IzMDI5ZDNhMjRiZjlhOTVhMTc4MDhmZTBlZGY2My5qcGc?x-oss-process=image/format,png#pic_center)

------

## 网站开启伪静态

**步骤：宝塔进入网站设置 -> 伪静态，把代码复制进去 -> 网站后台开启去掉地址栏中的/?/**

```nginx
if (!-f $request_filename){
    set $rule_0 1$rule_0;
}
if (!-d $request_filename){
    set $rule_0 2$rule_0;
}
if ($rule_0 = "21"){
    rewrite ^/(.*) /?/$1 last;
}
```



**如图：**
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSGIwMzg4Mjk5ZWJkNjQ4ZTlhYWU1ZTRlY2Q2YzExZDA1Wi5qcGc?x-oss-process=image/format,png#pic_center)
![img](https://i2.wp.com/imgconvert.csdnimg.cn/aHR0cHM6Ly9hZTAxLmFsaWNkbi5jb20va2YvSGJjNDk1Y2U1NzQ3MjRjM2M5N2VmZmQ4MTUyYjFiYmVkcy5qcGc?x-oss-process=image/format,png#pic_center)

------







**如果不设置定时清除缓存，你需要经常到后台取刷新缓存。当然这个操作不是必须的，你可以不设置这两个命令。oneindex使用起来还是很方便的，如果对安装还是有疑问，可以看这张gif动画安装图：**



[宝塔面板安装oneindex | 码农家园 (codenong.com)](https://www.codenong.com/cs107112828/)