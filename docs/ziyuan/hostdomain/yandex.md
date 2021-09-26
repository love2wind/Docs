## 前言

前面给大家分享了[mail.ru免费域名邮箱的申请教程](https://love2wind.cn/archives/2185.html)，今天我们给大家再分享俄罗斯的另一家公司Yandex的免费域名邮箱的申请及设置过程。

Yandex域名邮箱是由俄罗斯互联网公司[Yandex](https://yandex.com)提供的一项免费服务。Yandex使用方便，比较稳定，收发信成功率也比较高。另外，Yandex也是目前为数不多的几家还保留着对SMTP/POP3/IMAP的支持的免费域名邮箱了。

## 注册账号

### 1）进入yandex邮箱网站

打开https://mail.yandex.com，点击黄色的 `Create an account`按钮。

![创建Yandex帐号](https://www.daweibro.com/sites/default/files/inline-images/01-yandex-create-an-account_0.png)

### 2）按照下图填写个人信息

依次填写名（Frist name）、姓（Surname)、用户名（Enter a login）、密码（Enter a password）、确认密码（Confirm password）、、手机号码（Mobile phone number）记得手机号码前面加上国家代码，国内手机是＋86，点击 `Send code` 发送验证码，把手机收到的验证码填写到验证码（Enter the code from the SMS）这一栏点击` Confirm` 验证，如果没有问题会提示`Your phone number successfully confirmed` 表明你的手机验证成功了，最后点击`Register` 进行注册。在弹出的小框里点击 `Accept` 接受隐私政策和使用条款，页面跳转后就直接进入邮箱了。

![Yandex确认手机验证码](https://www.daweibro.com/sites/default/files/inline-images/03-yandex-confirm-sms-code.png)

### 3）注册完成

这时我们就有了一个Yandex的账号的同时，我们也有了一个 `你的用户名@yandex.com` 的邮箱，和其他的邮箱基本操作没什么区别，很容易上手，不过这不是我们的主要目的，大家只要记着账号和密码就可以了，接下来我们就添加域名邮箱。

## 添加域名邮箱

### 1）进入域名邮箱控制台

打开https://connect.yandex.com/pdd/，填写域名，然后点击 `Sign up free` 。

![Yandex添加域名](https://www.daweibro.com/sites/default/files/inline-images/05-yandex-add-domain.png)

2.在新的页面，会有部分俄文看不懂，不过没关系，看到自己的域名下面有个“not confirmed”，点击进去，就会到了域名验证的环节了。

![Yandex添加域名待确认](https://www.daweibro.com/sites/default/files/inline-images/06-yandex-add-domain-02.png)

3.域名验证环节是验证你对域名的所有权和控制权的。有四种方法：

方法一：按照指定的文件名和内容，在域名的网站根目录下，创建一个html文件。确保这个文件能够从浏览器正常打开后，点击Check验证。

这个方法适合有正在运营的网站的朋友，简单快速，几乎是立马完成的，是大伟哥采用和推荐的方法。

![Yandex域名验证](https://www.daweibro.com/sites/default/files/inline-images/07-yandex-domain-check.png)

方法二：按照指定的内容，在网站的首页源代码里，插入一个meta元素。确认网页头部源代码里包含这个名字为“yandex-verification”的元素后，点击Check验证。

标签元素只要加在首页就好，其他页面不需要。这个一般需要更改网站的模版文件，有些麻烦，而且内容页面里加个这玩艺总感觉不干净，因此大伟哥不推荐。

方法三：进入域名注册商的管理界面，把自己域名的Whois信息里各个电子邮件修改成之前在Yandex申请的邮箱。

如果你的域名只是用来作为电子邮箱使用而没有开通网站，那么可以使用这种方法。不过要使用这一方法，得取消域名的隐私保护功能，因些大伟哥也不推荐这个方法。

方法四：进入域名注册商的域名管理界面，按照Yandex指定的格式，添加一个TXT的DNS记录。

这个方法在没有网站的情况下比方法三要好，能够保护域名注册人的隐私。不过DNS的解析生效是需要时间的，因此域名的验证可能要等一段时间。

以上四种方法，任选一种完成之后，你的手机就会收到一条短信：“【英富必】Your domain abcdefg.com has been confirmed in Yandex.Connect回复TD退订”，这样域名验证就成功了。

## 五、配置邮箱的DNS记录

还记得如何修改域名的DNS记录吗？可以先到《[解析域名到自己的VPS/云服务器](https://www.daweibro.com/node/15)》来复习一下。

要使Yandex的域名邮箱生效，我们需要添加2条DNS记录。

\1. 一个MX记录，子域名为“＠”，值为“mx.yandex.net.”，优先度为“10”

\2. 一个CNAME记录，子域名为“mail”，值为“domain.mail.yandex.net.”优先度不填

注意，官方说明里要求保留DNS值里的实心句点，但是实际上不同域名注册商的域名管理界面操作起来可能不一样，以大伟哥使用的namesilo来说，如果保留实心句点，提交的时候就会报错：“mx.yandex.net. must be a valid host”，如果去掉最后的小数点，就能保存成功了。实际上后面有小数点是对的，但是很多域名管理面板里加记录并不需要，原因是域名系统在解析的时候会自动给你加上。这一点不用纠结。

还有，＠这个符号也一样，可能你在子域名里填写了，但是查看记录的时候子域名却是空白，这也是没有关系的。

## 六、防止发出的邮件被当成垃圾邮件

MX记录生效以后，原则上就可能通过邮件服务器收发电子邮件了。但是还有很重要的一步不能省略，那就是添加SFP记录和DKIM记录。

1.SPF是指Sender Policy Framework，是为了防范垃圾邮件而提出来的一种DNS记录类型，SPF是一种TXT类型的记录。SPF记录的本质，就是向收件人宣告：本域名的邮件从清单上所列IP发出的都是合法邮件，并非冒充的垃圾邮件。

进入域名管理界面，管理DNS记录，添加一个TXT记录，子域名为“＠”，值为“v=spf1 redirect=_spf.yandex.net”。

2.DKIM 技术通过在每封电子邮件上增加加密的数字标志，然后与合法的互联网地址数据库中的记录进行比较。当收到电子邮件后，只有加密信息与数据库中记录匹配的电子邮件，才能够进入用户的收件箱。它还能检查邮件的完整性，避免黑客等未授权者的修改。 DKIM 的基本工作原理同样是基于传统的密钥认证方式，他会产生两组钥匙，公钥(public key)和私钥(private key)，公钥将会存放在 DNS 中，而私钥会存放在寄信服务器中。

我们要做的就是把公钥加入DNS记录里面。

进入域名管理界面，添加一个TXT记录，子域名为“mail._domainkey”，对应的值填写的是DKIM签名，是一个很长的字符串，可以到https://connect.yandex.com/portal/services/mail找到。格式为“v=DKIM1; k=rsa; t=s; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCJVxN5dM/oOXkwkW7feP31ykg1My7ArR23Z17Nd6CLpuXcBZ2N77fcvuo404MKHryHpIiT5FYuI1KF2TyUeESYZTRsfsduEbIW+vzUX4wk3T4Nj0oHr6FWmEnwlypNeZTlvaXM7nBEexWf8d5Xtm2z4a4lAlc/VdWkBVmHPfo9xQIDAQAB”，只是参考，不能照搬哦。

这两个记录解析生效同样需要时间，最短数分钟，最长可能需要3天。

## 七、分配自定义邮箱地址

终于可以自定义域名邮箱了，这里是你自己的天下，admin＠daweibro.com，i@daweibro.com, daweibro@daweibro.com等等等等,想用什么用什么，不需要因为重名的原因加上一些难看的数字字母。

配置自定义邮箱的网址是https://connect.yandex.com/portal/admin，我们需要给组织添加一个新成员并分配新的邮箱地址。在页面左下角点击“Add”->“Add a person”:

![Yandex添加组织成员](https://www.daweibro.com/sites/default/files/inline-images/08-yandex-add-email-01.png)

2.依次输入新成员的姓名并分配邮箱地址，并设置用户登录密码，最后点击Add就完成了。

![创建Yandex域名邮箱](https://www.daweibro.com/sites/default/files/inline-images/09-yandex-employee-info.png)

## 八、启用新邮箱并设置客户端收发邮件

还差一步就大功告成了。要启用新邮箱，需要通过网页登陆一次，登陆过程中需要同意使用协议和隐私政策，才能真正激活邮箱。

登录的入口是：https://mail.yandex.com，直接输入之前设置的邮箱地址和密码就可以了。

第一次会弹出一个如下的窗口，选中方框并点击下面的“Complete Registration”，这样电子邮件就算激活了，接下来会自动进入邮箱。

![Yandex完成注册](https://www.daweibro.com/sites/default/files/inline-images/10-yandex-complete-registration.png)

## 九、本地邮件客户端及网站发信设置参数

千辛万苦地去申请一个免费并支持POP3/IMAP/SMTP协议的域名邮箱，不就是为了方便快捷地和外国友人建立业务联系嘛！使用Thunderbird/Outlook等本地邮件客户端软件是必须滴，使用Drupal/WordPress/Magento等网站程序通过SMTP自动发送邮件也是必不可少滴。以下是Yandex域名邮箱服务器的各种协议参数：

IMAP：imap.yandex.com 端口：993(SSL)
POP3：pop.yandex.com 端口：995(SSL)
SMTP：smtp.yandex.com 端口：465(SSL)