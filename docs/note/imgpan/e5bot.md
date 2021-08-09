## 前言

Office365 E5申请好之后，如何稳定续期是个玄学问题，除了搭建各种列表程序调用api保持活跃以外，今天我们来试试利用E5SubBot来续期，至于Office365 E5 如何申请可以看这篇文章：

> [Office365 E5 开发者订阅免费申请](tech/e5)

## 简介

🤖E5SubBot 是 Office365 E5 自动续订机器人，通过Telegram BOT自动调用Outlook API尝试自动续订E5订阅(每三小时调用一次) ，程序基于Golang + MySQL。

**地址：**https://github.com/iyear/E5SubBot

**作者搭建的BOT:** https://t.me/E5Sub_bot

**交流群组：**https://t.me/e5subbot

**特性：**

- 自动续订E5订阅(可自定义的调用频率)
- 可管理的简易账户系统
- 完善的任务执行反馈
- 极为方便的授权方式

**原理：**由于E5订阅是开发者订阅，只要调用相关API，保持API的活跃就有可能续期，本程序就是通过调用 Outlook ReadMail API 实现玄学的续订方式，不保证续订效果。

## 使用

!> 由于本方法需要使用的Telegram，所以在整改操作过程中会出现一些你懂的网络故障，这个就要你自己想办法解决了，不会的可以搜索。

#### 1、获取应用信息

?> 目前微软经常会关闭快速注册应用的通道，所以E5SubBot自带的流程会经常性抽风，所以推荐大家手动注册应用并绑定。下面说下基本流程。

![](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/af96723cc15ce17f4a5449d543032ad6.png)



> 1. 进入https://azure.microsoft.com/zh-cn/
> 2. 右上角`登录`
> 3. 点击右上角`门户`
> 4. 点击中间“管理`Azure Active Directory`下的`查看`
> 5. 点击左侧箭头，在扩展栏里选择`应用注册`
> 6. 点击`新注册`
> 7. 名称随便填，选择“ 任何组织目录(任何Azure AD 目录- 多租户)中的帐户和个人Microsoft 帐户(例如，Skype、
>    Xbox)”，重定向URI 类型选Web 输入框填`http://localhost/e5sub`
> 8. 记好应用程序(客户端) ID（即Client_id）
> 9. 点击侧边栏的`证书和密码`，选择`新客户端密码`
> 10. 说明随便填，截止期限自己选择，点`完成`
> 11. **保存好客户端密码！！！保存好客户端密码！！！保存好客户端密码！！！**此密码只显示一
>     遍（客户端密码就是Client_secret）
> 12. 点击侧栏`API 权限`，点击`添加权限`
> 13. 在右侧选`Microsoft Graph`
> 14. 点击`委托的权限`并在下面选择`openid`、`offline_access`、`mail.read`、`user.read`并添加
> 15. 点击`代表xxx 授予管理员同意`
> 16. 点击`是`并等待（不行就重复步骤15 和16 并刷新）

**至此，azure 应用申请的步骤完成！**


#### 2、绑定E5SubBot

首先打开作者搭建的BOT：https://t.me/E5Sub_bot（或者在**Telegram**中搜索`E5Sub_bot`）

1. 发送`/bind`，**不要点击链接**

2. 回复`client_id+空格+client_secret`（在前面步骤8 和步骤11中取得）

   - 打开授权链接，登录（建议用子账号，管理员也可以，最好用电脑）

   - 等待跳转，复制网址（不是登录网址，是跳转后浏览器地址栏中的网址，以`http://localhost/e5sub?code=`开头的一串字符）

3. 回复机器人`刚才复制的链接+空格+别名`（别名自己随便填写，方便记忆就好）
   如`http://localhost/e5sub?code=OAQABAAIAAAAGV_bv21oQQ4ROqh0_1-tAObGXtDgPSww8tJb4emamOwwCKkccit_Hs
   H5WCj37CGLJvN7IXlyXO8piHqtW1Yyg5aB_iVV9b1INX1WvaS1zDlXsKrDwq1f4vjPN2bulUarT0OmHh47ROl4JCUkRB8b
   G0dwJSP7FJDPWXXVSfoCFKM9oLNuDi-V6q3inpEz5FIGrYzn0RI34ka_Jp0j-bBCUZo_4Judw77Jzg9CssHnsjY7HBIYIr
   cZ-hHnNyWWzZ1-FERIl8A6AKWf8L_ch7B1f4nJTBtEvBEfAdcXMIN6dHyE0pNuJsAudQHkF0_Cr_Y-siNGndtAbMZm_vtB
   4cNyLUQQAoTDXxDP44l_NUsEq0B1_BRqQMRKObywUAqzZL70N2TB_p4mLGn_V3RkE1POFYNoMSU-CEgRR5Auoz1aQlEcTe
   RsCOwV02KLYDJoyy1hEq6UIHnkb3EebND3fvdYV2FQ6R0LwULBPN7VotTXi2vG2KGEAA-O4foiIlDEOoOQGO7uke1L-owh
   BHiIHiyv4VfEnCoEvxAQrlEN-NvXcjKD6xG2z8BJGvsDY8O11VU4V1zVcEQFiu4mJxHKfsgwHVJ2SiMoLvATeOigsRCHF8
   Vl1cQeBDM8EsROLFoBY_78gAA&session_state=a422855f-af51-4578-9ecf-76da5caa6175 测试别名`

看下图，就是整个绑定流程

![绑定E5SubBOT](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/4f535b6fcd4bc13ca2a2f2690f4fb9b4.png)



#### BOT常用命令

- `/my` 查看已绑定账户信息
- `/bind`  绑定新账户
- `/unbind` 解绑账户
- `/export` 导出账户信息(JSON)
- `/help` 帮助
- `/task` 手动执行一次任务（**管理员** ）
- `/log` 获取最近日志文件（**管理员**）

## 部署

!> 推荐大家利用作者搭建的bot来绑定自己的账号自动续订，首先是使用方便，作者随时更新迭代，其次本程序的部署安装相对来说比较复杂，虽然而且作者也提供了比较方便的docker版本，但是对大部分用户来说门槛还是比较高的，最后主要的一点是**懒**。如果你想折腾，可以使用作者提供的docker版本自己部署搭建，下面来简单说说流程。

#### docker环境

宝塔面板安装好docker管理器，安装好docker-compose

#### Docker部署

宝塔面板安装好docker管理器，安装好docker-compose，这个请自行搜索解决。

#### docker部署

使用如下命令开始部署：

```shell
mkdir ./e5bot && wget --no-check-certificate -O ./e5bot/config.yml https://raw.githubusercontent.com/iyear/E5SubBot/master/config.yml.example
vi ./e5bot/config.yml
wget --no-check-certificate https://raw.githubusercontent.com/iyear/E5SubBot/master/docker-compose.yml
docker-compose up -d
```

如果第一次失败，可以使用 `docker-compose restart`重启一次。

#### 二进制文件

上面的docker部署好之后，在[Releases](https://github.com/iyear/E5SubBot/releases)页面下载对应系统的二进制文件，上传至服务器，

Windows: 在cmd中启动 `E5SubBot.exe`

Linux使用如下命令执行文件：

```shell
screen -S e5sub
chmod +x E5SubBot
./E5SubBot
(Ctrl A+D)  //快捷键，切换出监控窗口
```

如果提示screen: command not found 命令不存在，可以执行：`yum install screen` 或 `apt-get install screen`安装。

#### 部署配置

docker安装是自动配置好`config.yml`文件的，编码为UTF-8。配置模板的说明如下：

```yaml
#bindmax,notice,admin,errlimit可热更新，直接更新config.yml保存即可
#更换为自己的BotToken
bot_token: xxxxx
#不需要socks5代理删去即可
socks5: 127.0.0.1:1080
#公告，合并至/help
notice: "第一行\n第二行"
#管理员tgid，前往https://t.me/userinfobot获取，用,隔开
#管理员权限: 手动调用任务，获得任务总反馈
admin: 66666,77777,88888
#任务最大出错次数，满后自动解绑账户并发送通知，无限次数将值改为负数(-1)即可
#以ms账户为单位，不会解绑所有账户(只解绑错误账户)
#主要为了减少资源浪费.bot重启后会清零所有错误次数
errlimit: 5
#API调用频率，使用cron表达式
cron: "1 */3 * * *"
#最大可绑定数
bindmax: 3
#mysql配置，请提前创建数据库
mysql:
  host: 127.0.0.1
  port: 3306
  user: e5sub
  password: e5sub
  database: e5sub
```

注意：docker里面的mysql信息可以不用修改。

`bindmax`,`notice`,`admin`,`goroutine`,`errlimit`可热更新，直接更新`config.yml`保存即可

| 配置项    | 说明                                                         | 默认值 |
| --------- | ------------------------------------------------------------ | ------ |
| bot_token | 更换为自己的`BotToken`                                       | -      |
| socks5    | `Socks5`代理,不需要删去即可.例如:`127.0.0.1:1080`            | -      |
| notice    | 公告.合并至`/help`                                           | -      |
| admin     | 管理员`tgid`，前往 https://t.me/userinfobot 获取，用`,`隔开;管理员权限: 手动调用任务，获得任务总反馈 | -      |
| goroutine | 并发数，不要过大                                             | 10     |
| errlimit  | 单账户最大出错次数，满后自动解绑单账户并发送通知，不限制错误次数将值改为负数`(-1)`即可;bot重启后会清零所有错误次数 | 5      |
| cron      | API调用频率，使用cron表达式                                  | -      |
| bindmax   | 最大可绑定数                                                 | 5      |
| mysql     | mysql配置，请提前创建数据库(旧版本升级请设置table为users，否则读不到数据表) | -      |

#### 注意事项

> 更新时间与北京时间不符

更改服务器时区为`Asia/Shanghai`，然后使用`/task`手动执行一次任务刷新时间

> 绑定格式错误

不要带"+"号

> 错误:Can't create more than max_prepared_stmt_count statements (current value: 16382)

没有关闭`db`导致触发`mysql`并发上限，请更新至`v0.1.9`

> 长时间运行崩溃

疑似内存泄露，尚未解决，请自行采用守护进程运行或定时重启`Bot`

## 结语

如果不用docker安装，你还需要安装go语言环境，总的来说自己折腾还是有点门槛的，建议用作者的bot来续订。

续订的效果是个很玄学的问题，建议，在安装oneindex来保证下使用的频率。

这只是一种续订的方法，但是不敢保证效果，你只能试试看。