![img](https://sunpma.com/usr/uploads/2020/07/2852525402.jpg)

## 说明

**此脚本安装的是绿色版，安装卸载都非常简单，并配置有`TLS`域名伪装；**
**GitHub：https://github.com/sunpma/mtp**

## 安装

**执行如下代码进行安装**

```
# 创建程序目录并进入
mkdir /home/mtproxy && cd /home/mtproxy

# 下载程序并配置安装
curl -s -o mtproxy.sh https://raw.githubusercontent.com/sunpma/mtp/master/mtproxy.sh && chmod +x mtproxy.sh && bash mtproxy.sh
```

**安装过程：**

```
=========================================
请输入一个客户端连接端口 [1-65535]
(默认端口: 443):433（说明：自定义链接端口）

---------------------------
port = 443
---------------------------

请输入一个管理端口 [1-65535]
(默认端口: 8888):8888（说明：自定义管理端口）

---------------------------
manage port = 8888
---------------------------

请输入一个需要伪装的域名：
(默认域名: azure.microsoft.com):azure.microsoft.com（说明：自定义TLS伪装域名）
状态码：302

---------------------------
伪装域名 = azure.microsoft.com
---------------------------

请输入你需要推广的TAG：
若没有,请联系 @MTProxybot 进一步创建你的TAG
(留空则跳过):（说明：默认跳过或输入TAG）

---------------------------
PROXY TAG = 
---------------------------

配置已经生成完毕!
TMProxy+TLS代理: 运行中
服务器IP：132.145.91.50
服务器端口：65534
MTProxy Secret:  xxxxxx
TG一键链接: https://t.me/xxxxxx
TG一键链接: tg://xxxxxx
=========================================
```

# 使用

```
# 进入程序目录
cd /home/mtproxy

# 运行
bash mtproxy.sh start

# 调试
bash mtproxy.sh debug

# 停止
bash mtproxy.sh stop

# 重启
bash mtproxy.sh restart
```

# 卸载

**因为是绿色版卸载极其简单，直接删除程序目录即可；**

```
rm -rf /home/mtproxy
```

## 开机启动

**编辑`/etc/rc.local`开机自启服务文件，将如下代码添加到开机自启脚本中；**

```
# 编辑自启文件
vi /etc/rc.local

# 添加如下代码
bash /home/mtproxy/mtproxy.sh start > /dev/null 2>&1 &
```