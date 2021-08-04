# 常用脚本及用法收集

## WARP

**查看WARP当前统计状态：`wg`**

**查看当前IPV4 IP：`curl -4 ip.p3terx.com`**

**查看当前IPV6 IP：`curl -6 ip.p3terx.com`**

**手动临时关闭WARP网络接口**

```
wg-quick down wgcf
```

**手动开启WARP网络接口**

```
wg-quick up wgcf
```

**启动`systemctl enable wg-quick@wgcf`**

**开始`systemctl start wg-quick@wgcf`**

**重启`systemctl restart wg-quick@wgcf`**

**停止`systemctl stop wg-quick@wgcf`**

**关闭`systemctl disable wg-quick@wgcf`**

## [①EUserv](https://github.com/YG-tsj/EUserv-warp)

##### **恢复EUserv官方DNS64（重装系统者，可直接跳到第二步脚本安装）**

```
echo -e "search blue.kundencontroller.de\noptions rotate\nnameserver 2a02:180:6:5::1c\nnameserver 2a02:180:6:5::4\nnameserver 2a02:180:6:5::1e\nnameserver 2a02:180:6:5::1d" > /etc/resolv.conf
```

**仅支持Debian 10/Ubuntu 20.04系统，根据自己需求选择以下脚本1或者脚本2**

##### **脚本1：IPV4是WARP分配的IP，IPV6是VPS本地IP**

```
wget -qO- https://cdn.jsdelivr.net/gh/YG-tsj/EUserv-warp/warp4.sh|bash
```

##### **脚本2：IPV4与IPV6都是WARP分配的IP**

```
wget -qO- https://cdn.jsdelivr.net/gh/YG-tsj/EUserv-warp/warp64.sh|bash
```

##### **IPV6 VPS专用分流配置文件(以下默认全局IPV4优先，IP、域名自定义，详情见视频教程)**

```
{ 
"outbounds": [
    {
      "tag":"IP6-out",
      "protocol": "freedom",
      "settings": {}
    },
    {
      "tag":"IP4-out",
      "protocol": "freedom",
      "settings": {
        "domainStrategy": "UseIPv4" 
      }
    }
  ],
  "routing": {
    "rules": [
      {
        "type": "field",
        "outboundTag": "IP4-out",
        "domain": [""] 
      },
      {
        "type": "field",
        "outboundTag": "IP6-out",
        "network": "udp,tcp" 
      }
    ]
  }
}
```

## [②Oracle甲骨文脚本集合，针对KVM X86架构/ARM架构](https://github.com/YG-tsj/Oracle-warp)

#### 1、root一键脚本

用户名：root，密码自定义。方便登录与编辑文件！！后续再次执行脚本意味着更改root密码！！

提示：密码不要设置得过于简单，容易被破解。密钥文件要保存好，以防万一！

**统一适用于纯IPV4、纯IPV6、双栈IPV4+IPV6，非root状态下直接输入以下脚本（已测试支持甲骨文与谷歌云）**

```
bash <(curl -sSL https://cdn.jsdelivr.net/gh/YG-tsj/CFWarp-Pro/root.sh)
```

#### 2、warp多功能一键脚本

**支持X86/ARM架构的纯IPV4、纯IPV6、双栈IPV4+IPV6 VPS脚本**

```
wget -N --no-check-certificate https://cdn.jsdelivr.net/gh/YG-tsj/CFWarp-Pro/multi.sh && chmod +x multi.sh && ./multi.sh
```

进入脚本快捷方式 `bash multi.sh`

#### 3、其他KVM架构VPS查看专用ip方式（待更新）

脚本5不用输入专用IP。其他脚本需要输入专用IP（防止VPS本地IP套WARP后失联），根据不同的VPS，专用IP可能是IP，也可能是IP段。

**进入**SSH查看专用IP命令：

```
ip -4 route`或者`ip addr
```

结果会显示IP或者IP段，IP段用 /数字 表示！

例：有的VPS公网IP为123.456.2.3，而专用IP段可能就是123.456.0.1/16，此时，要输入的专用IP就是123.456.0.1/16，别忘记输入后面的/16哦！

#### 4、如果Mark-a脚本安装错误执行下方操作即可

一键V2:
`bash <(curl -s -L https://git.io/v2ray-setup.sh)`

一键XV2:
`bash <(curl -sL https://s.hijk.art/xray.sh)`

**先装第一个脚本 ，卸载后再装第二个脚本卸载在装8合一就能解决**

## [③mack-a](https://github.com/mack-a/v2ray-agent)

- 支持快捷方式启动，安装完毕后，shell输入**`vasma`**即可打开脚本，脚本执行路径**`/etc/v2ray-agent/install.sh`**
- **Latest Version【推荐】**

```
wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh
```

- **Stable-v2.4.32**

```
wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/fd4daa2cc88dc687b4a7d0a64c4ea7d984290938/install.sh" && chmod 700 /root/install.sh && /root/install.sh
```

- **Stable-v2.2.24**

```
wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/9ae23c13a56460d8c14f27c8eb65efc73b173f46/install.sh" && chmod 700 /root/install.sh && /root/install.sh
```

## [④SKY-BOX](https://github.com/BlueSkyXN/SKY-BOX)

## 使用方法

wget -O box.sh https://raw.githubusercontent.com/BlueSkyXN/SKY-BOX/main/box.sh && chmod +x box.sh && clear && ./box.sh

```
wget -O box.sh https://raw.githubusercontent.com/BlueSkyXN/SKY-BOX/main/box.sh && chmod +x box.sh && clear && ./box.sh
```

### ARM beta使用方法

```
wget -O box.sh https://raw.githubusercontent.com/BlueSkyXN/SKY-BOX/main/armbox.sh && chmod +x box.sh && clear && ./box.sh
```

## [⑤NEZHA](https://github.com/naiba/nezha)

```
curl -L https://raw.githubusercontent.com/naiba/nezha/master/script/install.sh  -o nezha.sh && chmod +x nezha.sh
sudo ./nezha.sh
```

**国内镜像加速：**

```
curl -L https://cdn.jsdelivr.net/gh/naiba/nezha@master/script/install.sh -o nezha.sh && chmod +x nezha.sh
CN=true sudo ./nezha.sh
```

## ⑥MTPROTO

```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/mtproxy.sh && chmod +x mtproxy.sh && bash mtproxy.sh
```

## ⑦其他

**工具箱：**

```
bash <(curl -s -L http://file.twovps.co/cs)
```

**配置一览：**

```
bash <(wget -qO- git.io/ceshi)
```

**流媒体解锁：**

```
bash <(curl -sSL "https://github.com/CoiaPrant/MediaUnlock_Test/raw/main/check.sh")
```

**YABS：**

```
curl -sL yabs.sh | bash
```

**LemonBenchIntl：**

```
wget -O- https://ilemonra.in/LemonBenchIntl | bash -s full
```

## ⑧系统命令

`apt-get update`
升级安装包相关的命令,刷新可安装的软件列表(但是不做任何实际的安装动作)

`apt-get upgrade`
进行安装包的更新(软件版本的升级)

`apt-get dist-upgrade`
进行系统版本的升级(Ubuntu版本的升级)

`do-release-upgrade`
Ubuntu官方推荐的系统升级方式,若加参数-d还可以升级到开发版本,但会不稳定

⑨⑩