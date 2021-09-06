## 🎈写在前面

首先祝大家国庆节中秋节双节快乐！

好久没更新了，今天蹭着国庆节休息，~~更新一篇。~~ 水一篇。

## 🎏教程

之前我记得好伙伴问了下怎么加谷歌的思源宋体，网上方法很多，有自己上传字体直接引用、或者用有字库里面的js简单快速，但我认为最好用的那就是引用谷歌字体的API了。

!> 谷歌中文字体api地址：https://fonts.google.com/?subset=chinese-simplified

进入Noto Serif SC思源宋体的界面：

[![谷歌字体api思源宋体](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/9469ba54ef1e24802fdc429d863a23cb.png)](https://picup.heson10.com/img/upyun/image-20201001225452635.png)

在这里就像超市挑选商品一样，选择一款自己喜欢的字体样式。

点击后面的`select this style` 浏览器地址栏就是接下来需要引用的api链接了。

我这边选的是400（普通）和900**（加粗）**的样式，结合异步加载代码，引用地址如下：

```
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;900&display=swap" rel="stylesheet" media="print" onload="this.media='all'">

 
```

把以上代码放入模板的`<head></head>`之间。同时设置字体css：

```
font-family: 'Mulish', -apple-system, 'Noto Serif SC', "PingFang SC", "Microsoft Yahei UI", "Microsoft Yahei", sans-serif;

 
```

以上代码是我博客用的字体，mulish是一款英文字体，一般放在中文字体前面（也是谷歌的英文字体，引用方法同上），效果：

[![mulish字体效果](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/img/62784cd59162984220ee6937386b70ce.png)](https://picup.heson10.com/img/upyun/image-20201001230423198.png)

经过测试，`fonts.googleapis.com`还是比 `loli`的节点要更快点。

## 🎀关于异步加载多说一句

前面加载api里面可以看到比一般加载方式多了2个参数

- `media="print"`
- `onload="this.media='all'"`

```
media="print"`意思是打印的时候才能看见，当页面刚加载的时候，只能看见后备字体，也就是我这边设置的`PingFang SC
```

`onload="this.media='all'"`当所有文档、css加载完毕之后，把`media="print"`设置为`media="all"`，这样以来就能看到刚刚设置的思源宋体了。

这样刚打开页面的时候，就不会出现那种字体群魔乱舞的情况了。💔

###### 参考文章：`https://io-oi.me/tech/loading-google-fonts-async/`