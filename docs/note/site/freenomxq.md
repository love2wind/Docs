众所周知，Freenom是地球上唯一一个提供免费顶级域名的商家，不过需要每年续期，每次续期最多一年。由于我申请了一堆域名，而且不是同一时段申请的， 所以每次续期都觉得折腾，于是就写了这个自动续期的脚本。

## 🍭 效果

![邮件截图](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/95db23d0395eae0719bcc9a0e1b690db.webp)

无论是续期成败或者脚本执行出错，都会收到的程序发出的邮件。如果是续期成败相关的邮件，邮件会包括未续期域名的到期天数等内容。 邮件参考了微信发送的注销公众号的邮件样式。

## 🎁 事前准备

- 发信邮箱：为了方便理解又称机器人邮箱，用于发送通知邮件。目前支持`Gmail`、`QQ邮箱`以及`163邮箱`，程序会自动判断发信邮箱类型并使用合适的配置。
- 收信邮箱：用于接收机器人发出的通知邮件。推荐使用`QQ邮箱`，`QQ邮箱`唯一的好处只是收到邮件会在`QQ`弹出消息。
- VPS：随便一台服务器都行，系统推荐`Centos7`，另外PHP版本需在`php7.2`及以上。
- 没有了

## 📪 配置发信邮箱

下面分别介绍`Gmail`、`QQ邮箱`以及`163邮箱`的设置，你只用看自己需要的部分。注意，`QQ邮箱`与`163邮箱`均使用账户加授权码的方式登录， `谷歌邮箱`使用账户加密码的方式登录，请知悉。另外还想吐槽一下，国产邮箱你得花一毛钱给邮箱提供方发一条短信才能拿到授权码。

#### 设置Gmail

1、在`设置>转发和POP/IMAP`中，勾选

- 对所有邮件启用 POP
- 启用 IMAP

![gmail配置01](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/15bd3d5798d4433b13de2f4a1708021b.webp)

然后保存更改。

2、允许不够安全的应用

登录谷歌邮箱后，访问 [谷歌权限设置界面](https://myaccount.google.com/u/0/lesssecureapps?pli=1&pageId=none) ，启用允许不够安全的应用。

![gmail配置02](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/f1752253a0922a0c252bfea87af0c6f4.webp)

另外，若遇到提示

> 不允许访问账户

登录谷歌邮箱后，去 [gmail的这个界面](https://accounts.google.com/b/0/DisplayUnlockCaptcha) 点击允许。这种情况较为少见。

#### 设置QQ邮箱

在`设置>账户>POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务`下，开启`POP3/SMTP服务`

![qq邮箱配置01](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/dcd6437c2d28b98acd3af1c9e2610cb5.webp)

此时坑爹的QQ邮箱会要求你用手机发送一条短信给腾讯，发送完了点一下`我已发送`

![qq邮箱配置02](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/ba30690e9359d2c22dfa3953f922efb5.webp)

然后你就能看到你的邮箱授权码了，使用邮箱账户加授权码即可登录，记下授权码

![qq邮箱配置03](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/326881bc412b04a130ed6ed3a5776d3c.webp)

![qq邮箱配置04](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/77574cd7a97319702cc8cc5dc5beae72.webp)

#### 设置163邮箱

在`设置>POP3/SMTP/IMAP`下，开启`POP3/SMTP服务`和`IMAP/SMTP服务`并保存

![163邮箱配置01](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/a33fdaae5b631a20b446abe0d526a1f2.webp)

![163邮箱配置02](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/18f1df290e6116b87ae52742eb922226.webp)

现在点击侧边栏的`客户端授权密码`，并获取授权码，你看到画面可能和我不一样，因为我已经获取了授权码，所以只有`重置授权码`按钮，这里自己根据网站提示申请获取授权码，网易和腾讯一样恶心，需要你用手机给它发一条短信才能拿到授权码

![163邮箱配置03](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/ecf7f66f6f7be364049e5b8d4c6e60ca.webp)

163 邮箱送信后，接收方如果没收到可以在垃圾邮件里面找一下。

#### Telegram bot

上面介绍了三种邮箱的设置方法，如果你不想使用邮件推送，也可以使用 Telegram bot，灵活配置。在`.env`文件中， 将`TELEGRAM_BOT_ENABLE`的值改为`true`，即可启用 Telegram bot，同样的，将`MAIL_ENABLE`的值改为`false`即可关闭邮件推送方式。 Telegram bot 有两个配置项，一个是`chatID`（对应`.env`文件中的`TELEGRAM_CHAT_ID`）， 通过使用你的 Telegram 账户发送`/start`给`@userinfobot`即可以获取自己的id， 另一个是`token`（对应`.env`文件中的`TELEGRAM_BOT_TOKEN`），你的 Telegram bot 令牌，你会创建 Telegram bot 就知道怎么获取， 不多赘述。如何创建一个 Telegram bot 请参考：[官方文档](https://core.telegram.org/bots#6-botfather)

## 🕹 通过腾讯云函数（SCF）部署

------

### 1、下载 SCF 版本的压缩包

此版本为特别版，支持通过腾讯云函数部署，与主分支版本不兼容，版本号为`v0.3_scf`，下载地址： https://github.com/luolongfei/freenom/archive/refs/tags/v0.3_scf.zip

下载后解压到你能找到的任意目录，你将得到一个文件夹，后期将通过文件夹的形式上传到腾讯云函数。

### 2、创建腾讯云函数

直接访问腾讯云函数控制台创建云函数： https://console.cloud.tencent.com/scf/list-create ， 按照下图所示的说明进行创建。

[![scf01](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/40f6c2739689dd542c32abda4927972d.webp)](https://z3.ax1x.com/2021/06/01/2nKCF0.png)

按照上图所示部署完成后，可以点击云函数的名称进入云函数管理画面，管理画面往下翻可看到`部署`与`测试`按钮，点击`测试`，稍等几秒钟，即可看到输出日志， 根据输出日志判断配置以及部署是否正确。

![scf02](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/d48fcd7dad3f72564abd34c286fb16d6.webp)

*有关腾讯云函数部署的内容结束。*

只要你完全按照上述教程走下来，应该就OK了，妈妈再也不会担心我的Freenom域名过期了。