之前本站的音乐播放器使用的是[APlayer插件](https://github.com/zgq354/APlayer-Typecho-Plugin)，今天无意中发现一个只需加载JS，即可调用 [APlayer](https://aplayer.js.org/) 和 [Meting](https://github.com/metowolf/MetingJS)，不依赖插件和服务器计算存储，任意站点都可使用的来播放 `网易云`，`QQ 音乐`，`酷狗`，`虾米`，`百度` 以及 `自定义的` 单曲和歌单的方法，在此记录并分享给大家。



## 引入 JS

将代码加入到主题对应的 `header.php` 中的 `</head>` 标签前即可

```html
<script>
    // APlayer API
    document.addEventListener('DOMContentLoaded', initAplayer);
    window.aplayers = window.aplayers || [];
    function initAplayer(option) {
        const common = {
            loadResource: function (id, resource, type) {
                return new Promise(function (resolve, reject) {
                    let loaded = document.head.querySelector('#' + id);
                    if (loaded) {
                        resolve('success: ' + resource);
                        return;
                    }
                    const element = document.createElement(type);
                    element.onload = element.onreadystatechange = () => {
                        if (!loaded && (!element.readyState || /loaded|complete/.test(element.readyState))) {
                            element.onload = element.onreadystatechange = null;
                            loaded = true;
                            resolve('success: ' + resource);
                        }
                    }
                    element.onerror = function () {
                        reject(Error(resource + ' load error!'));
                    };
                    if (type === 'link') {
                        element.rel = 'stylesheet';
                        element.href = resource;
                    } else {
                        element.src = resource;
                    }
                    element.id = id;
                    document.getElementsByTagName('head')[0].appendChild(element);
                });
            },
            loadResources: function (callback) {
                const loadResource = this.loadResource;
                const pt = '//s0.pstatp.com/cdn/expire-1-M/';
                const jd = '//cdn.jsdelivr.net/npm/';
                const resources = [
                    pt + 'aplayer/1.10.1/APlayer.min.css',
                    pt + 'aplayer/1.10.1/APlayer.min.js',
                    jd + 'meting@2/dist/Meting.min.js'
                ];
                const loadPromises = [];
                resources.forEach(resource => {
                    loadPromises.push(loadResource(btoa(resource).replace(/[=+\/]/g, ''), resource,
                        ({
                            'css': 'link',
                            'js': 'script'
                        })[resource.split('.').pop()]
                    ));
                });
                Promise.all(loadPromises).then(
                    function () {
                        if (typeof callback !== 'function') return;
                        let flag = false;
                        const waitAM = setInterval(() => {
                            if (!flag
                                && typeof APlayer === 'function'
                                && typeof MetingJSElement === 'function') {
                                flag = true;
                                callback();
                                clearInterval(waitAM);
                            }
                        }, 100);
                    }
                );
            },
            createAplayers: function (sources) {
                for (let i = 0; i < sources.length; i++) {
                    const child = document.createElement('div');
                    sources[i].parentNode.insertBefore(child, sources[i]);
                    sources[i].style.display = 'none';
                    const songsTag = sources[i].querySelectorAll('s');
                    const songs = [];
                    songsTag.forEach(songTag => {
                        const song = {};
                        for (let i = 0; i < songTag.attributes.length; i++) {
                            song[songTag.attributes[i].name] = songTag.attributes[i].value;
                        }
                        songs.push(song);
                    });
                    const options = { container: child, preload: 'none', autoplay: false, audio: songs };
                    const optionMap = sources[i].attributes;
                    for (let i = 0; i < optionMap.length; i++) {
                        options[optionMap[i].name] = optionMap[i].value;
                    }
                    this.loadResources(() => window.aplayers.push(new APlayer(options)));
                }
            }
        };

        if (option == 'manual') return new Promise((resolve, reject) => {
            common.loadResources(() => resolve('success'));
        });

        const aps = document.querySelectorAll('ap');
        if (aps.length !== 0) common.createAplayers(aps);

        const mts = document.querySelectorAll('meting-js');
        if (!window.refreshing && mts.length !== 0) common.loadResources(
            function () {
                mts.forEach(mt => {
                    if (!mt.aplayer) {
                        const html = mt.outerHTML;
                        mt.aplayer = { destroy: new Function(), list: { index: undefined } };
                        mt.outerHTML = '\n' + html;
                    }
                });
                document.querySelectorAll('meting-js').forEach(mt => {
                    let flag = false;
                    const waitMT = setInterval(() => {
                        if (!flag && mt.aplayer) {
                            flag = true;
                            window.aplayers.push(mt.aplayer);
                            console.log('replaced unloaded aplayer.')
                            clearInterval(waitMT);
                        }
                    }, 300);
                });
            }
        );
    }
</script>

<script>
    // PJAX 相关 BUG
    document.addEventListener('DOMContentLoaded', function () {
        let flag = false;
        window.needReloadUrls = window.needReloadUrls || new Set();
        const jqueryWaitor = setInterval(() => {
            if (!flag && jQuery) {
                flag = true;
                $(document).on('pjax:start', function () {
                    if (!window.refreshing || !window.pjaxStarted) {
                        window.pjaxStarted = true;
                        console.log('pjax:start');
                        window.aplayers.forEach(ap => {
                            ap.list.index = undefined;
                            ap.destroy();
                        });
                        window.aplayers = [];
                        setTimeout(() => window.pjaxStarted = false, 2000);
                    }
                });
                $(document).on('pjax:end', function () {
                    if (document.querySelector('meting-js')
                        || document.querySelector('.collapse-block')
                        || document.querySelector('#toggle-menu-tree')
                        || document.querySelectorAll('.content-tab-title').length > 1
                    ) {
                        if (!window.needReloadUrls.has(location.href)) {
                            window.needReloadUrls.add(location.href);
                            console.log('captured a neededReloadUrl.');
                        }
                    }
                });
                $(document).on('pjax:popstate', function (event) {
                    if (event.state && window.needReloadUrls.has(event.state.url) && !window.refreshing) {
                        window.refreshing = true;
                        console.log('back-forward handler.');
                        $.pjax.reload({
                            url: location.href,
                            container: '#body',
                            fragment: '#body',
                            scrollTo: false,
                            timeout: 8000
                        });
                        setTimeout(() => window.refreshing = false, 2000);
                    }
                });
                clearInterval(jqueryWaitor);
            }
        }, 500);
    });
</script>
```



如果你开启了 `PJAX`，可能需要单独加入回调函数。将 `initAplayer();` 添加进回调函数即可。

## 演示效果

### 网易云歌单

```
!!!
<!-- 引入方式 -->
<meting-js auto="https://music.163.com/#/playlist?id=110459831"></meting-js>
!!!
```

<meting-js auto="https://music.163.com/#/playlist?id=110459831"></meting-js>


### QQ音乐歌单

```
!!!
<!-- 引入方式 -->
<meting-js auto="https://y.qq.com/n/yqq/playlist/7355087593.html"></meting-js>
!!!
```

<meting-js auto="https://y.qq.com/n/yqq/playlist/7355087593.html"></meting-js>




### 自定义歌单

```
!!!
<!-- 标签引入 -->
<ap>
<s
    name="rainymood"
    artist="rainymood"
    url="https://rainymood.com/audio1110/0.m4a"
    cover="https://rainymood.com/i/badge.jpg">
</s>
</ap>
!!!

!!!
<!-- 或编程引入 -->
<div id="ap"></div>
<script>
    initAplayer('manual').then(() => {
        window.aplayers.push(new APlayer({
            container: document.querySelector('#ap'), preload: 'none', autoplay: false, audio: [
                {
                    name="rainymood",
                    artist="rainymood",
                    url="https://rainymood.com/audio1110/0.m4a",
                    cover="https://rainymood.com/i/badge.jpg"
                }
            ]
        }));
    });
</script>
!!!
```


<div id="ap"></div>
<script>
    initAplayer('manual').then(() => {
        window.aplayers.push(new APlayer({
            container: document.querySelector('#ap'), preload: 'none', autoplay: false, audio: [
                {
                    name="rainymood",
                    artist="rainymood",
                    url="https://rainymood.com/audio1110/0.m4a",
                    cover="https://rainymood.com/i/badge.jpg"
                }
            ]
        }));
    });
</script>


怎么样，效果还算不错吧，赶紧也给你添加一下啊。本文转载自[任意站点引入 APlayer 和 Meting 的简单方法](https://logi.im/blog/simple-way-to-add-aplayer-on-your-website.html)