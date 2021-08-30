## 前言

前段时间听说这个Docker，奈何没时间也就没有怎么研究，今天实属无聊，就研究了一下并写下了这篇指南

## 开始

> 这里我使用服务器的系统为Ubuntu18，不同系统的命令可能有所不同

### 准备

1.服务器（Linux或Windows Server2019及以上系统）或家用电脑（Linux或Windows 10及以上系统）

2.SSH连接软件

### 连接服务器并安装Docker

建议使用**Xshell**进行连接，界面美观简洁，连接后安装Docker

> 因为不同系统Docker的安装方式不同，这里我给出网络上Docker安装教程

[Docker安装 教程 ](https://www.runoob.com/docker/docker-tutorial.html)

> 当然，你如果安装了宝塔面板，你也可以在宝塔面板里安装Docker，方法也很简单，到**宝塔面板**-**软件商城**-下载**Docker管理器**，本插件自带Docker

### 安装并配置青龙面板

#### 青龙面板的安装

1. 

   ##### 拉取镜像

```
docker pull whyour/qinglong:latest
```

[![image.png](https://pic.rmb.bdstatic.com/bjh/5c8c444e10996a0702c9924328014b6d.png)](https://pic.rmb.bdstatic.com/bjh/5c8c444e10996a0702c9924328014b6d.png)

[image.png](https://pic.rmb.bdstatic.com/bjh/5c8c444e10996a0702c9924328014b6d.png)



1. 

   ##### 部署镜像

```
docker run -dit \
   -v $PWD/ql/config:/ql/config \
   -v $PWD/ql/log:/ql/log \
   -v $PWD/ql/db:/ql/db \
   -p 5700:5700 \
   --name qinglong \
   --hostname qinglong \
   --restart always \
   whyour/qinglong:latest
```

[![image.png](https://pic.rmb.bdstatic.com/bjh/5507c0490bd8f38f5ceb1f7b685d9096.png)](https://pic.rmb.bdstatic.com/bjh/5507c0490bd8f38f5ceb1f7b685d9096.png)

[image.png](https://pic.rmb.bdstatic.com/bjh/5507c0490bd8f38f5ceb1f7b685d9096.png)



#### 配置青龙面板

- 

  ##### 登录面板

  面板地址：http://服务器IP:5700

  默认账号：admin

  默认密码：adminadmin

  当您使用以上密码首次登录后，面板会显示已初始化密码

  请在SSH终端内查看新密码（输出的结果就是实际的密码了
  {"username":"admin","password":""），查看代码如下

  `docker exec -it qinglong cat /ql/config/auth.json`

- 青龙面板基础命令

(容器内执行或者新建定时任务时忽略docker exec -it qinglong)

更新青龙

```
docker exec -it qinglong ql update
```

更新青龙并编译

```
docker exec -it qinglong ql restart
```

拉取自定义仓库

```
docker exec -it qinglong ql repo https://ghproxy.com/https://github.com/whyour/hundun.git "quanx" "tokens|caiyun|didi|donate|fold|Env"
```

拉取单个脚本

```
docker exec -it qinglong ql raw https://ghproxy.com/https://raw.githubusercontent.com/moposmall/Script/main/Me/jx_cfd.js
```

删除7天前的所有日志

```
docker exec -it qinglong ql rmlog 7
```

启动bot

```
docker exec -it qinglong ql bot
```

导出互助码

```
docker exec -it qinglong ql code
```

通知测试

```
docker exec -it qinglong notify test test
```

立即执行脚本

```
docker exec -it qinglong task test.js now
```

并行执行脚本

```
docker exec -it qinglong task test.js conc
```

------

- 

  ##### 添加库

  > 进入青龙面板-定时任务-添加任务，将以下代码填入命令，定时规则请自己百度填写，添加完点击刚刚添加的那个任务上的开始图标，就会自动拉取库中脚本

青龙拉取常用京东脚本库

国内代理： [https://ghproxy.com/](https://ghproxy.com/https://raw.githubusercontent.com/sngxpro/QuanX/master/task/AllinOne.json)

【Faker集合仓库】

```
ql repo https://ghproxy.com/https://github.com/shufflewzc/faker2.git "jd_|jx_|getJDCookie" "activity|backUp" "^jd[^_]|USER|ZooFaker_Necklace"
```

【Faker仓库依赖库修复】SSH运行：

```
docker exec -it QL bash -c "apk add --no-cache build-base g++ cairo-dev pango-dev giflib-dev && cd scripts && npm install canvas --build-from-source"
```

【curtinlv仓库】

```
ql repo https://github.com/curtinlv/JD-Script.git
```

【star】

```
ql repo https://github.com/star261/jd.git "scripts" "code"
```

【lxk0301】已私有，以下链接为备份库。柠檬代维护库。

```
ql repo https://github.com/shufflewzc/jd_scripts-2.git "jd_|jx_|getJDCookie" "activity|backUp" "^jd[^_]|USER"
```

【龙珠】

```
ql repo https://github.com/longzhuzhu/nianyu.git "qx" “main”
```

【混沌】

```
ql repo https://github.com/whyour/hundun.git "quanx" "tokens|caiyun|didi|donate|fold|Env"
```

【passerby-b】（需要配合专用ck文件）

```
ql repo https://github.com/passerby-b/JDDJ.git "jddj_" "scf_test_event" "jddj_cookie"
```

【温某某】

```
ql repo https://ghproxy.com/https://github.com/shufflewzc/Wenmoux.git
```

【柠檬（胖虎）】

```
ql repo https://github.com/panghu999/panghu.git "jd_"
```

【zoopanda（动物园）】以下为备份库

```
ql repo https://github.com/shufflewzc/zoo.git "zoo"
```

【Ariszy（Zhiyi-N）】

```
ql repo https://github.com/shufflewzc/Ariszy.git "JD"
```

【ddo（hyzaw）】貌似已经删库 以下为备份

```
ql repo https://ghproxy.com/https://github.com/shufflewzc/hyzaw.git "ddo_"
```

[![image.png](https://pic.rmb.bdstatic.com/bjh/70ec266f27be0625f5e05a33231d0eb2.png)](https://pic.rmb.bdstatic.com/bjh/70ec266f27be0625f5e05a33231d0eb2.png)

[image.png](https://pic.rmb.bdstatic.com/bjh/70ec266f27be0625f5e05a33231d0eb2.png)

[![image.png](https://pic.rmb.bdstatic.com/bjh/14eb1c488b77a8cbed8cd9a3dee637d1.png)image.png](https://pic.rmb.bdstatic.com/bjh/14eb1c488b77a8cbed8cd9a3dee637d1.png)[![image.png](https://pic.rmb.bdstatic.com/bjh/a655c43c2e772dab405b07399cc2fdcd.png)image.png](https://pic.rmb.bdstatic.com/bjh/a655c43c2e772dab405b07399cc2fdcd.png)



点击运行，完成仓库拉取

### 添加Cookie

点击面板主页-环境变量-添加变量
变量名称为**JD_COOKIE**，值为京东Cookie数据（格式为 `pt_key=xxx;pt_pin=xxx;`（分号;不可少））

京东Cookie可通过以下途径获取
教程来源自网络，非本人制作

1.电脑获取：[https://drive.raycns.com/%E8%B5%84%E6%BA%90%E7%9B%98/%E6%96%87%E6%A1%A3/%E9%80%9A%E8%BF%87%E7%94%B5%E8%84%91%E6%8A%93%E5%8F%96%E4%BA%AC%E4%B8%9C%E6%89%8B%E6%9C%BACookies%E7%A4%BA%E4%BE%8B(8.4%E6%96%B0%E7%89%88).docx](https://drive.raycns.com/资源盘/文档/通过电脑抓取京东手机Cookies示例(8.4新版).docx)
2.手机获取：[https://drive.raycns.com/%E8%B5%84%E6%BA%90%E7%9B%98/%E6%96%87%E6%A1%A3/%E9%80%9A%E8%BF%87%E6%89%8B%E6%9C%BA%E6%8A%93%E5%8F%96%E4%BA%AC%E4%B8%9CCookies%E6%95%99%E7%A8%8B%E6%96%B9%E5%BC%8F%E4%BA%8C(2020.8.13%E7%89%881).docx](https://drive.raycns.com/资源盘/文档/通过手机抓取京东Cookies教程方式二(2020.8.13版1).docx)

## 后语

大概就这些，如有不全，或不理解之处，烦请百度！！！

如果你需要搭建JDC扫码登录，我这里有相应教程，但要收费，价格不贵，物有所值！用了我很多时间