**说明：**`AriaNg`算是`Aira2`中博主认为最好用的一个`Web`前端面板，连接支持`Http(s)`或`Websocket(Security)`协议，如果我们使用`https`域名访问`AriaNg`面板，那会强制你使用`Https`和`Websocket`(安全)协议，最早期的面板是不会强制的，不过用的话，肯定是用最新版的，这时候就需要对`Aria2`简单的配下证书了，然后才能使用`Https`、`Websocket`(安全)协议进行连接，这里就水下方法。

## 方法

**1、申请SSL证书**

```
提示：如果安装Aria2的服务器有现成的HTTPS站点，可以跳过该步骤，直接使用该站点域名。
```

先解析一个域名到安装`Aria2`的服务器，然后申请`SSL`，方法如下：

```
1、宝塔面板：左侧网站-添加站点-站点设置-SSL-申请Let's Encrypt。
2、LNMP安装包：自己使用命令添加域名的时候，有申请SSL选项。
```

如果服务器只安装了`Aria2`或者没有`Web`环境，这时候可以使用`Caddy`申请，使用命令：

```
#安装Caddy
curl https://getcaddy.com | bash -s personal
#申请SSL，将后面修改成自己的域名和邮箱
caddy -host www.moerats.com -email admin@moerats.com -agree
```

这里要注意的是，对于`CentOS`系统，还需要开启`80`端口，不然使用`Caddy`签发证书会失败，开启如下：

```
#CentOS 6
iptables -I INPUT -p tcp --dport 80 -j ACCEPT
service iptables save
service iptables restart

#CentOS 7
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --reload
```

申请成功后的`SSL`证书路径如下：

```
#具体以自己域名为准
/root/.caddy/acme/acme-v02.api.letsencrypt.org/sites/www.moerats.com
```

我们就可以发现域名的`crt`和`key`证书文件。

**2、修改配置文件**
编辑`Aria2`配置文件`aria2.conf`，如果不知道路径的，可以使用命令查找：

```
find / -name aria2.conf
```

修改如下：

```
#是否启用RPC服务的SSL/TLS加密
rpc-secure=true
#申请的域名crt证书文件路径，自行修改
rpc-certificate=/home/www.moerats.com.crt
##申请的域名key证书文件路径，自行修改
rpc-private-key=/home/www.moerats.com.key
```

如果配置文件没有以上参数的，可以手动添加，修改完成后，重启`Aria2`生效即可，此时`Https`和`Websocket`(安全)协议就都可以用了，然后`AriaNg`配置`RPC`信息的时候，直接填写域名、密匙即可。

**常规方式**

Aria2的RPC功能开启HTTPS,需要给aria2配置证书，然后修改aria2.conf

```
rpc-secure=true
rpc-certificate=(.pem文件路径)
rpc-private-key=(.key文件路径)
```


配置中总有人会一直失败，无法链接，然后还不知道哪里出错。
下面就介绍一个取巧的办法快速开启HTTPS链接Aria2。

**反向代理大法好**

对，就是使用NGINX反向代理开启HTTPS。

**1.首先你需要给网站配置SSL证书。（这个没什么好说的）**

**2.在NGINX网站配置中添加**

```nginx
location ^~ /jsonrpc {
    proxy_http_version 1.1;
    add_header Front-End-Https on;
    proxy_set_header Connection "";
    proxy_set_header Host $http_host;
    proxy_set_header X-NginX-Proxy true;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://127.0.0.1:6800/jsonrpc;
    proxy_pass_header X-Transmission-Session-Id;
}
```



**3.在面板中设置RPC地址端口为443**

例如这样：

![aria2_https](https://img.naiel.cn/uploads/big/2e143616ad2b3bd6bfffe39a4d09a0c9.png)

aria2_https

这样就完工了，非常简单的取巧办法。
使用反向代理RPC，这样通信不需要通过6800端口，所以在防火墙上可以关闭6800端口。