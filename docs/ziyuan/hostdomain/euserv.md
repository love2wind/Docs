# EUserv纯IPV6德国免费VPS申请全攻略

## EUserv简介

EUserv是一家德国的老牌主机运营商，提供服务器托管、VPS，云服务，网站托管和域名注册等多种服务。其中就有一款深受国人~~喜爱~~（迫害）免费产品`VS2-free`，配置如下：

| 项目 |      配置      |
| :--: | :------------: |
| CPU  | 1 Core @ 1 GHz |
| 内存 |      1GB       |
| 硬盘 |    10GB HDD    |
| 带宽 |     1 Gbit     |
|  IP  |     1IPV6      |

官网地址：https://www.euserv.de

## 注册前准备

注册过程比较简单，大家按照下面的步骤一般都能成功，因为是人工审核，所以过不过就很难说了，其中有下面几点需要注意的事项一定要注意，否则100%过不了。

- 尽量使用国外的Email，如Gmail，微软邮箱。国内的现在基本见一个死一个。
- 由于国内封杀比较严重，所以还是不要用国内身份注册的好。可以使用http://www.haoweichi.com/或者https://www.fakeaddressgenerator.com/等美国身份生成网站获取身份信息。
- IP地址要和身份统一。比如说你用美国IP登录，那你的身份信息就必须填写美国的，以后在登录网站面板时也尽量用注册时的IP地址登录。所以你可能需要科学上网才能申请成功。
- 必须允许 EUserv 给你发送广告邮件，否则会删号。
- 审核时间是数小时至两天不等，通过了就会发邮件，没通过就会直接删号无任何通知，被删号的邮箱不能再次使用。
- 使用免费VPS的用戶必须每月登录后台給VPS進行免费续期。

## 开始注册

### 1、进入注册页面

进入官网首页，上面的菜单栏找到`vServer`，然后在下拉菜单找到`VS2-free`，点击进入免费VPS注册页面。

或者直接进入申请地址：https://www.euserv.com/en/virtual-private-server/root-vserver/v2/vs2-free.php

### 2、确认订单

点击`Order`，然后会弹出订购框，再次点击一下`Order`（如下图所示）

![Snipaste_2021-09-22_17-57-03](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/ee085b5b1d31bc52faaab5fafdb1498d.webp)

### 3、开始结算并验证邮箱

点击完`Order`后耐性等待一阵就会弹出确认结算的页面，点击 `Go to checkout` 按钮，然后在后面的页面选择 `Register` ，并输入你的Email邮箱地址，点击 `Send new PIN to Email Address` 按钮，这时系统会给你的邮箱发送一个验证码，在下面填入验证码，点击 `Confirm PIN` 按钮。

![Snipaste_2021-09-22_18-40-46](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/052507166539e5c5240f1ca58a5a7af1.webp)

### 4、填写身份信息并注册

邮箱通过验证后，我们就可以开始填写身份信息了，这里必须要认真填写并牢记。

![Snipaste_2021-09-22_19-10-17](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/d5d982d591daf38d6ff625ffc379ef08.webp)

### 5、确认付款并完成注册

点击注册后就到了付款的页面，勾选 `I have read and accepted the terms and conditions and the rescission information.` 前的选择框，然后点击弹出的确认付款 `Proceed checkout` 按钮。

![Snipaste_2021-09-22_19-10-17](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/3ded80f3a9df7b2f65ca0e0e7b136e30.webp)

网页加载缓慢，这里耐心等待一下，不出意外就会弹出 `Thank you for your order. Please check your email-account for our confirmation.` 以及` continue shopping` 的蓝色按钮了，这时注册就算完成了。立刻就能收到发来的几封告知邮件。

## 登录并补充信息

完成注册这才是完成了一部分，下面我们要登录管理面板后台补充填写账号的身份信息并确认后才算是真的完成整个注册流程了。

### 1、登录后台

接着上面的步骤，点击` continue shopping` 的蓝色按钮，进入首页，在上方的菜单栏找到 `Login Customer Panel`后台登录菜单，或者直接点击下面的后台登录地址进行登录，填写Email和密码即可。

后台管理地址：https://support.euserv.com/

### 2、补充填写身份信息

客户信息里把国家、州、城市、地址、电话等信息填全（标*号的必须填写）才可以让订单生效。而且这些信息尽量要用真实的，并且国家要与IP地址一致。

![Snipaste_2021-09-22_19-37-11](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/0025cecba917f514594a7ad1cd81c5d6.webp)

### 3、保存后等待人工审核

上面信息都填完后，拉到下面点击 `Save` 按钮保存后，就要等人工审核通过了，时间数个小时到两三天不等，也有人说五六天以后通过了，反正我是没遇到，如果超过两天大概率就是GG了，成功的可能性极小。如果审核成功我们会收到通知邮件。

这时我们进入后台首页点击橙色` vServer` 按钮，就可以看到当前服务器的状态，`State` 栏目前是一个小沙漏，如果审核通过了，就是一个绿色对号图标，并且会显示服务器名称和IPV地址。

## EUserv常见问题

### 1、获取ROOT密码

进入管理后台首页，点击橙色` vServer` 按钮，下面的点击 `Select` 按钮，在控制面板左侧边栏找到 `configure ` 下面的 `Server data  `中可以找到。

`Default-Password for SSH or Webpanel` 对应的就是SSH密码

### 2、SSH登录

#### 1）利用嘿呦终端登录SSH

到嘿呦终端https://www.heyterm.com/这个网站注册帐号，并新建资产，将EUSERV的IPV6地址填进去。用户名是root,密码是前面SERVERDATA中的密码。

#### 2）利用手机热点登录SSH

把你的手机设为热点，然后电脑连接手机热点，再用XSHELL之类的进行连接，地址、用户名、密码都是一样的。

因为手机网络默认是有IPV6的，所以我们利用热点就可以直接登录。

#### 3）电脑端安装IPV6

这个可以到网上搜索下教程，设置起来比较麻烦，当然设置好了，以后登录就很方便。

#### 4）利用其他VPS设置跳板机来登录

这个方法呢适合有其他可以访问IPV6的主机的用户，设置起来也比较麻烦，不推荐。

### 3、重装系统

和前面一样，进入 `Server data ` 页面，找到 `Reinstallation` 进入系统安装界面。选择你要安装的系统（推荐Debian10），然后点击 `Stare Reinstallation` 按钮就会进行系统重装。不过EUserv的主机会间歇性失联，有时重装后等待几天都是常有的事情，如果重装没有反应，几天后再次重装一下说不定就好了。

![Snipaste_2021-09-22_20-37-24](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/88ed96cbeac95e5891b3a0693da37831.webp)

### 4、配置WARP实现IPV4/IPV6双栈访问

由于EUserv现在搞了个DIG9，有的主机原来的NAT64方法已经失效。幸好有大佬找到了更好的方法，那就是按照配置WARP，以此来实现IPV4/IPV6双栈访问。

**项目地址：**https://github.com/kkkyg/DJwarp

直接复制一键安装命令，按照提示操作就行了，非常方便。

### 5、自动续期

同样还是上面大佬的脚本，安装提示操作即可。

**项目地址：**https://github.com/kkkyg/EU666

### 6、更多玩法

- [纯IPV6服务器安装宝塔面板 – 搭建网站实现IPV4访问/ipv6，ipv4皆可访问](https://www.daniao.org/6927.html)
- [只有IPV6的VPS设置NAT64实现访问IPV4网络](https://haoduck.com/681.html)
- 期待你的新玩法

## 结语

总体来说，EUserv的可玩性不高，毕竟性能和带宽摆在那，但是，相对其他免费主机来说入门门槛也比较低，对于新手拿来练手是完全没有问题的。尤其是套上CF以后，当个备用机还是一个不错的选择。