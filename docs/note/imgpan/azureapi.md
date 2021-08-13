### 前言

现在各种网盘列表程序多入牛毛，OneIndex、PanIndex、OlaIndex、OneManager、ShareList、PyOne、OneList、CuteOne、Z-File等都是不错的选择，但是有个问题，就像OneIndex的作者删库了，注册引导页面随时会挂，而且微软有时也会关闭快速注册通道，导致很多人在安装过程中，出现未知错误。所以就要自己登录 Azure 注册应用获取API，这里就记录一下API申请过程，抛砖引玉，大家如果有更好的方法，可以在下面留言交流。当然，如果你的程序可以自动成功跳转申请，那么下面的方法也可以作为一个备用方案。

### 申请

#### 1. 登录 Azure

- 国际版打开 [https://portal.azure.com/](https://portal.azure.com/ ) ，登录你的微软账号，

- 世纪互联（中国大陆代理版），如果管理员开放申请 API 的话，打开 [https://portal.azure.cn](https://portal.azure.cn/)，登录你的微软账号

点击 `管理 Azure Active Directory` 下的 `查看`按钮，或者下面的**Azure服务**下的`Azure Active Directory`（如果有的话）

![img](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/c50c9713880746509c26cb1bd99c3ec8.webp)

#### 2. 注册应用

在左侧列表中选择 `应用注册`，

![](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/3b8cb652ab2c0818b87d65b728bf860f.webp)

点击`+新注册`，注册一个新应用，信息按如下填写：

> **名称：**无所谓，你自由发挥
>
> **受支持的帐户类型：** `任何组织目录(任何 Azure AD 目录 - 多租户)中的帐户和个人 Microsoft 帐户(例如，Skype、Xbox)`
>
> **重定向 URI (可选)：**根据你使用的 OneDrive 目录索引程序对应填入
>
> - OneIndex：作者删库，改为你自己程序的域名，必须为 SSL（在 `controller\AdminController.php` 文件大概第 186 行的位置）
> - OLAINDEX：https://olaindex.ningkai.wang 或 https://your.domain/callback
> - OneManager：https://scfonedrive.github.io
> - Cloudreve：https://your.domain/api/v3/callback/onedrive/auth
> - Z-File：https://zfile.jun6.net/onedrive/callback

![img](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/9fec60718e322d6364fb9bc785ca702b.webp)

#### 3. 获取 Client_id

创建完成后，复制 `应用程序(客户端) ID`，这就是你的 client_id

![img](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/f552be12281989af1f39553147b2b50c.webp)

#### 4. 添加 API 权限

点击下方的 `查看API权限 - 添加权限`，找到 `Microsoft Graph - 委托的权限`，搜索 `file` 全部打勾，添加权限

![img](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/feeb05d6954aaf5c4e2fbc085a23e6e0.webp)

#### 5. 创建 Client_secret

最后点击左侧的 `证书和密码 - 客户端密码 - 新建客户端密码`，添加一个客户端密码，截止期限选择 `永不`，把生成的密码复制下来（此密码只显示一次），这是你的 client_secret

![img](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/49bec57a5b1c402fd178a6fe362e8f5a.webp)

## 完成

上面的流程走完，你就已经获取了列表程序需要的 `client_id` 和 `client_secret`，接下来填入你使用的列表程序对应的地方，按照安装指引安装即可。