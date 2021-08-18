# 哪吒监控透明效果主题

主题是我扒的，扒的一个修改版的哪吒，可能不太完美，但是使用应该没问题

我想把国旗和系统的图标搞下来，不好搞，估计 js 可以做到替换，但是我不会

扒下来一大堆东西，然后一个一个删掉多余的，顺便自己也改了点点，耗时几个小时。CSS 里面我搞了注释，你要修改自己的风格也就方便点

https://ii.do/43.html

#### 哪吒监控

https://github.com/naiba/nezha



#### 主题截图

![哪吒监控](https://cdn.jsdelivr.net/gh/idarku/img@main/1629254144992.jpg)



#### 主题演示

http://server.ii.do/



#### 主题代码

```html
<style>
/* 屏幕适配 */

@media only screen and (min-width: 1200px) {
  .ui.container {
    width: 77%;
  }
}

@media only screen and (max-width: 767px) {
  .ui.card>.content>.header:not(.ui), .ui.cards>.card>.content>.header:not(.ui) {
    margin-top: 0.5em;
  }
}



/* 图标颜色和大小*/

i.icon {
        color: #000;
        width: 1em !important;
}



/* 菜单颜色 */

.ui.large.menu {
    background-color: rgba(255, 255, 255, 55%);
}

.ui.dropdown .menu {
  border: 0;
  border-radius: 0px;
  background-color: rgba(255, 255, 255, 55%);
}



/* 登录按钮颜色 */

.nezha-primary-btn {
    background-color: #21ba45 !important;
    color: #fff;
}



/* 背景图片 */

body {
 content: " ";
  background: fixed;
  z-index: -1;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-position: top;
  background-repeat: no-repeat;
  background-size: cover;
  background-image: url(https://cdn.jsdelivr.net/gh/idarku/img@main/1628656119298.jpg);
}



/* 大卡片 */

#app .ui.fluid.accordion {
    background-color: #fbfbfb26;
    border-radius: 0.4rem;
}



/* 小卡片 */

.ui.four.cards>.card {
    border-radius: 0.6rem;
    background-color: #fafafaa3;
}



/* 小卡片右上角图标颜色 */

.nezha-secondary-font {
  color: rgba(252, 166, 7, 0.952) !important;
}



/* 小卡片右上角图标位置 */

.ui.right.center.popup {
  margin: -3px 0 0 0.914286em !important;
  -webkit-transform-origin: left 50%;
  transform-origin: left 50%;
}
.ui.bottom.left.popup {
  margin-left: 1px !important;
  margin-top: 3px !important;
}
.ui.top.left.popup {
  margin-left: 0;
  margin-bottom: 10px !important;
}
.ui.top.right.popup {
  margin-right: 0;
  margin-bottom: 8px !important;
}
.ui.left.center.popup {
  margin: -3px .91428571em 0 0 !important;
  -webkit-transform-origin: right 50%;
  transform-origin: right 50%;
}



/* 弹出来的卡片 */

.status.cards .ui.content.popup {
    border-radius: 0.35rem;
    background-color: rgba(255, 255, 255, 85%);
}
.ui.content {
  margin: 0;
  padding: 1em !important;
}



/* 弹出来的小卡片位置 */

.status.cards .flag {
  margin-right: 0 !important;
}
.status.cards .header > .info.icon {
  float: right;
  margin-right: 0;
  cursor: pointer;
}
.status.cards .wide.column {
  padding-top: 0 !important;
  padding-bottom: 0 !important;
  height: 2rem !important;
}
.status.cards .three.wide.column {
  padding-right: 0 !important;
}
.status.cards .wide.column:nth-child(1) {
  margin-top: 1rem !important;
}
.status.cards .wide.column:nth-child(2) {
  margin-top: 1rem !important;
}
.status.cards .description {
  padding-bottom: 1rem !important;
}
.status.cards .ui.content.popup {
  min-width: 292px;
  min-width: 21rem;
}
.status.cards .outline.icon {
  margin-right: -4px;
}



/* 进度条圆角和颜色 */

.ui.progress{border-radius:50rem}
.ui.progress .bar {
  min-width: 1.8em !important;
  border-radius: 15px;
  line-height: 1.65em;
  }

.ui.fine.progress> .bar {
  background-color: #21ba45!important;
}
.ui.progress> .bar {
  background-color: #000!important;
}
.ui.progress.fine .bar {
  background-color: #21ba45!important;
}
.ui.progress.warning .bar {
  background-color: #ff9800!important;
}
.ui.progress.error .bar {
  background-color: #e41e10!important;
}
.ui.progress.offline .bar {
  background-color: #000!important;
}



/* 上传下载图标颜色 */

i.arrow.alternate.circle.down.outline.icon {
    color: green;
}

i.arrow.alternate.circle.up.outline.icon {
    color: #ff0000;
}



/* 奶妈的版权 */

.ui.inverted.segment, .ui.primary.inverted.segment {
    color: #000;
    font-weight: bold;
    background-color: rgba(255, 255, 255, 25%)
}
</style>
<script>
window.onload = function(){
var footer=document.querySelector("div.footer-container")
footer.innerHTML="©2021 涅槃服务器监控 & Powered by 哪吒监控"
footer.style.visibility="visible"
}
</script>
<script>
window.onload = function(){
var avatar=document.querySelector(".item img")
var footer=document.querySelector("div.is-size-7")
footer.innerHTML="奶妈监控面板 and 我扒的CSS"
footer.style.visibility="visible"
avatar.src="https://cdn.jsdelivr.net/gh/idarku/blog@20210723/favicon.ico"
avatar.style.visibility="visible"
}
</script>
```

#### 使用方法

\1. 用哪吒的默认主题，复制上方主题代码，粘贴到自定义代码里面保存即可

\2. 实在不懂找奶妈，我只是个打工人



[哪吒监控面板主题分享-美国VPS综合讨论-全球主机交流论坛 - Powered by Discuz! (hostloc.com)](https://hostloc.com/thread-880548-1-2.html)