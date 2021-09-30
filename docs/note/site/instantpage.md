![](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/3042e6d83bd92e0d9e81f285474e624c.webp)

今天不知道写点啥，刚才看网站后台，发现加载了个**instant.page**的JS，干脆就水一篇关于instant.page的文章吧。

### 关于instant.page

> instant.page官网：https://instant.page

instant.page宣称可让网站加载时间缩短到 1 分钟以内，并提高 1% 的转化率。其作用是可以预加载用户想访问的页面，当用户真正点击链接后，就会直接从缓存中读取，以此提升网站的访问速度。

instant.page 原理的话我们不必深层了解，只需知道：

- 使用即时预加载技术，在用户点击之前预先加载页面。当用户的鼠标悬停在一个链接上超过 65 毫秒时，浏览器会对此页面进行预加载，当用户点击链接后，就从预加载的缓存中直接读取页面内容，从而达到缩短页面加载时间的目的。
- instant.page 是渐进式增强 - 对不支持它的浏览器没有影响。
- **使用 instant.page 会显著增加自己的网站的 PV 以及请求量。**
- **使用 instant.page 只会预加载 html 页面，而不会加载图片等资源。因此点击预加载的页面是秒开的，图片在点击之后才会加载，不用担心与 lazyload 的各种不兼容问题。**

### 使用方法

#### 一、使用官方提供的带有 Cloudflare 加速的脚本

建议服务器在国外的朋友使用。只要把这行代码添加到网站的 `</body>标签`之前即可。（**一般都可以在后台直接添加**）

```html
<script src="//instant.page/5.1.0" type="module" integrity="sha384-by67kQnR+pyfy8yWP4kPO12fHKRLHZPfEsiSXR8u2IKcTdxD805MGUXBzVPnkLHw"></script>
```

#### 二、使用国内公共CND

**Jsdelivr**

```html
<script src="//cdn.jsdelivr.net/npm/instant.page@5.1.0/instantpage.min.js"></script>
```

**字节跳动**

```html
<script src="//lf9-cdn-tos.bytecdntp.com/cdn/expire-1-M/instant.page/5.1.0/instantpage.min.js"></script>
```

```html
<script src="//s0.pstatp.com/cdn/expire-1-M/instant.page/1.2.2/instantpage.min.js" type="application/javascript"></script>
```

**BOOTCDN**

```html
<script src="https://cdn.bootcdn.net/ajax/libs/instant.page/5.1.0/instantpage.min.js"></script>
```

**二。自托管**

建议服务器在国内的朋友使用。只需将下面这段 js [点击查看](https://lf9-cdn-tos.bytecdntp.com/cdn/expire-1-M/instant.page/5.1.0/instantpage.min.js)上传到自己服务器，然后在 `</body>标签`之前根据路径添加下面的代码即可。

```html
<script src="`存放路径`/instantpage.min.js" type="module"></script>
```

### 参考文章

- [instant.page官网](https://instant.page/)
- [网站预加载JS脚本 instant.page ](https://www.zrahh.com/archives/399.html)
