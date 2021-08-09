众所周知，Freenom是地球上唯一一个提供免费顶级域名的商家，不过需要每年续期，每次续期最多一年。由于我申请了一堆域名，而且不是同一时段申请的， 所以每次续期都觉得折腾，于是就写了这个自动续期的脚本。

## 🍭 效果

![邮件示例](https://camo.githubusercontent.com/6fc6d19ebf59fcc4f7c598ee10239cf08ff1ab7c99c485d04400102af05e5031/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133395272642e706e67)

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

![gmail配置01](https://camo.githubusercontent.com/9dd9133768961d8588901418e90d6ad1db8d78337777d5b87c17d2e28b157c28/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133744b73672e706e67)

然后保存更改。

2、允许不够安全的应用

登录谷歌邮箱后，访问 [谷歌权限设置界面](https://myaccount.google.com/u/0/lesssecureapps?pli=1&pageId=none) ，启用允许不够安全的应用。

![gmail配置02](https://camo.githubusercontent.com/1ec85c95621bfc1683b4b6d290a37a1ae09ee7d6e6884983742934dff15c137f/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f313339324b482e706e67)

另外，若遇到提示

> 不允许访问账户

登录谷歌邮箱后，去 [gmail的这个界面](https://accounts.google.com/b/0/DisplayUnlockCaptcha) 点击允许。这种情况较为少见。

#### 设置QQ邮箱

在`设置>账户>POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务`下，开启`POP3/SMTP服务`

![qq邮箱配置01](https://camo.githubusercontent.com/d919fed60cb19ef83a4d12108aaa9c4224431b54393f5d7e2a543ce6ec477755/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f313363494b412e706e67)

此时坑爹的QQ邮箱会要求你用手机发送一条短信给腾讯，发送完了点一下`我已发送`

![qq邮箱配置02](https://camo.githubusercontent.com/f2875b489cef9c91cea4dad6fc2c54a3e9e5d1a68ffde368fe8ae2f009e179c8/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133633476642e706e67)

然后你就能看到你的邮箱授权码了，使用邮箱账户加授权码即可登录，记下授权码

![qq邮箱配置03](https://camo.githubusercontent.com/ed25fdf0dfda956cc8c23b50214c162cc648a45563c1cd66fa97b5b73ef34399/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133635462742e706e67)

![qq邮箱配置04](https://camo.githubusercontent.com/be02667e951699cc8a13841ce664d385dd67f20de46eb69d5b0b777b0d7a78d0/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133636f44492e706e67)

#### 设置163邮箱

在`设置>POP3/SMTP/IMAP`下，开启`POP3/SMTP服务`和`IMAP/SMTP服务`并保存

![163邮箱配置01](https://camo.githubusercontent.com/41ffb7ab319d5ec7ab64c0679eed59500f5ceb4f95e933ca74afe671b58abb9a/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133574b5a6e2e706e67)

![163邮箱配置02](https://camo.githubusercontent.com/79dab5c92eecb2f0b5926a52a6b15d7164d4bf4bd93eeaacfc3d4378d48d774c/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133575149302e706e67)

现在点击侧边栏的`客户端授权密码`，并获取授权码，你看到画面可能和我不一样，因为我已经获取了授权码，所以只有`重置授权码`按钮，这里自己根据网站提示申请获取授权码，网易和腾讯一样恶心，需要你用手机给它发一条短信才能拿到授权码

![163邮箱配置03](https://camo.githubusercontent.com/185fe465f20f4f41a4b38cce017c381cade18b2a912908551a75b13d654abd32/68747470733a2f2f73322e617831782e636f6d2f323032302f30312f33312f3133574d61712e706e67)

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

![scf01](https://camo.githubusercontent.com/4bd08db7e038f9f968a5be3025dceca064e6007e15cf8d22c92d39fd28d6c208/68747470733a2f2f7a332e617831782e636f6d2f323032312f30362f30312f326e4b4346302e706e67)

按照上图所示部署完成后，可以点击云函数的名称进入云函数管理画面，管理画面往下翻可看到`部署`与`测试`按钮，点击`测试`，稍等几秒钟，即可看到输出日志， 根据输出日志判断配置以及部署是否正确。

![scf02](https://camo.githubusercontent.com/dafab5ddf63b4eae8ab49430183505a2a4c312be0642f9ec97074a2a8f5fc99d/68747470733a2f2f7a332e617831782e636f6d2f323032312f30362f30312f326e475a33712e706e67)

*有关腾讯云函数部署的内容结束。*

只要你完全按照上述教程走下来，应该就OK了，妈妈再也不会担心我的Freenom域名过期了。