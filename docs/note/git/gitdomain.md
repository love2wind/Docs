## 前 言

Github自定义域名的方法网上一搜一大把，但是从18年开始Github的自定义域名支持HTTPS了，因为我一直在用CF解析并且强制HTTPS，一直没有发现什么问题，前段时间偶尔发现，我的git页面设置里的**Enforce HTTPS**选项是灰的，无法选择。然后就是一顿折腾，最后还是解决了。这里就大概记录下，顺便也就把自定义域名的方法也一并放上来吧。其实[官方文档](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)里写的很详细，只不过像我这种英语业余3级看起来还是有点费劲，能看懂的可以直接去研究。

#### 1. Github 支持的自定义域名类型

| 支持的自定义域名类型                | 域名例子                          |
| ----------------------------------- | --------------------------------- |
| www subdomain                       | `www.example.com`                 |
| one apex domain & one www subdomain | `example.com` & `www.example.com` |
| apex domain                         | `example.com`                     |
| custom subdomain                    | `blog.example.com`                |

#### 2. GitHub Pages 站支持的域名

| GitHub Pages 站类型        | 在 Github 上 Pages 的默认域名和主机地址 | 页面被如何重定向                                             | 自定义域名举例        |
| -------------------------- | --------------------------------------- | ------------------------------------------------------------ | --------------------- |
| User Pages                 | `username.github.io`                    | 自动重定向到设置的自定义域名                                 | `user.example.com`    |
| Organization Pages         | `orgname.github.io`                     | 自动重定向到设置的自定义域名                                 | `org.example.com`     |
| User Project Pages         | `username.github.io/projectname`        | 自动重定向到 User Pages 站自定义域名的子目录（`user.example.com/projectname`） | `project.example.com` |
| Organization Project Pages | `orgname.github.io/projectname`         | 自动重定向到 Organization Pages 站自定义域名的子目录（`org.example.com/projectname`） | `project.example.com` |

## 自定义域名

!> **这里以 User Pages 来说，比如我的个人Github页面`love2wind.github.io`。即 `<你的 github 用户名>.github.io`。对于组织来说，这个地址是 `<组织名称>.github.io`。

### Github Pages配置

![](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/Snipaste_2021-08-11_01-23-32.jpg)

#### 1. 开启 Github Pages 功能

如上图所示，①进入我的github仓库**love2wind.github.io**，在 `Settings` 中，②找到 `Pages` 设置项，③选择 `Source` 为对应的要部署的分支，这里分支我选择`master branch`，目录选`root`，**注意：**选择 `master branch` 会视 `/README.md` 为 web 的 `index.html`，选择 `master branch /docs folder` 会视 `/docs/README.md` 为 web 的 `index.html`。

#### 2. 配置中自定义域名

Ⅰ. 如上图④在 `Custom domain` 中添加自己的域名并保存，这里我填入`love2wind.com`

Ⅱ. 或者在项目分支中添加 `CNAME` 文件，`CNAME` 文件的内容为`love2wind.com`

!> 这里推荐第二种，尤其对于有设置 CI 的项目，因为 CI 上将第一种设置覆盖。

> 这一步是比较重要却又容易忽视的一步：
>
> - 如果添加到 GitHub Pages 中的是 `love2wind.com`，那么 `www.love2wind.com` 会被重定向到 `love2wind.com`；
> - 如果添加到 GitHub Pages 中的是 `www.love2wind.com`，那么 `love2wind.com` 会被重定向到 `www.love2wind.com`；

这里我选择重定向到 `love2wind.com`，所以设置为 `love2wind.com`

#### 3. SSL（HTTPS）配置

**强烈推荐开启**，勾选 `Enforce HTTPS`，Github 会自动保持 HTTPS 证书的有效。

!> 这里就是我前面提到的问题，如上图中所示，我的 `Enforce HTTPS`是灰的无法勾选，经过下面的操作，就可以勾选了。

![image-20210811020639101](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/image-20210811020639101.png)

> **按照官方提示，进行如下操作：**
>
> 1.  把 Custom domain 中的值清空，并点击 `Save` 进行保存；
> 2.  在 Custom domain 中的填入之前清空的值，我这里是 `love2wind.com` ，填入后点击保存；
> 3.  尝试在浏览器里主动访问 [https://love2wind.com](https://love2wind.com) ，地址要根据自己的情况，注意协议类型是 https，正确情况下是能正常访问的；
> 4.  刷新项目设置页，如果 `enforce HTTPS` 可勾选，勾选即可；
> 5.  如果 `enforce HTTPS` 不可勾选，并且提示 `Not yet available for your site because the certificate has not finished being issued”` ，说明证书尚未申请完成，等待一天即可。
>
> **注意**，如果使用 Chrome 访问 https://love2wind.com 地址栏左侧仍未出现小绿锁，请检查自己的网站引用的资源文件有没有使用了 http 协议，请替换成相应的 https 资源。

### 域名解析

添加 DNS 记录，为了能设置`Apex` 域名，需要在 DNS 中配置 A 记录指向 github 的 IP：

```accesslog
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

以上四条任意一条就行。

同时，设置 `CNAME` 记录将 `www.love2wind.com` 指向 `love2wind.github.io`。

## 写在最后

到这里一个完整的Github自定义域名、配置Pages、强制HTTPS的过程就记录完毕了，至于项目页面（User Project Pages）和组织页面、组织项目页面的配置过程都大同小异，就不一一列举了。

---

#### 参考

- [GitHub Pages 自定义域名实践整理](https://segmentfault.com/a/1190000018038675)

- [GitHub Pages 对自定义域名支持 HTTPS ](https://likfe.com/2018/05/03/github-pages-custom-domains-support-https/)

- [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

