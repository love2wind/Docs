## 安装要求

> 内存：512M以上，推荐768M以上（纯面板约占系统60M内存）
> 硬盘：300M以上可用硬盘空间（纯面板约占20M磁盘空间）
> 系统：CentOS 7.1+ (Ubuntu16.04+.、Debian9.0+)，确保是干净的操作系统，没有安装过其它环境带的Apache/Nginx/php/MySQL/pgsql/gitlab/java（已有环境不可安装）
> 架构：x86_64（主流服务器均是此架构），ARM不完整兼容（面板环境安装慢，部分软件可能安装不上）

**宝塔Linux面板7.7.0版本是基于Centos/Debian/Ubuntu开发的，为了最好的兼容性，请使用以上系统**
**系统兼容性顺序：**

> Centos7.x > Debian10 > Ubuntu 20.04 > Cenots8.x > Ubuntu 18.04 > 其它系统

!> 提示：Centos官方已宣布在2020年停止对Centos6的维护更新，各大软件开发商也逐渐停止对Centos6的兼容，新服务器不建议使用Centos6

推荐先安装 堡塔SSH客户端 (免费/简单/中文/多屏)

## Linux面板7.7.0安装命令

**Centos安装命令：**
```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```

**试验性Centos/Ubuntu/Debian安装命令** **独立运行环境（py3.7） 可能存在少量兼容性问题 不断优化中** 
```
curl -sSO http://download.bt.cn/install/install_panel.sh && bash install_panel.sh
```

**Ubuntu/Deepin安装命令：**
```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh
```

**Debian安装命令：**
```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh
```

**Fedora安装命令:**
```
wget -O install.sh http://download.bt.cn/install/install_6.0.sh && bash install.sh
```

**Linux面板7.7.0升级命令：**

```
curl http://download.bt.cn/install/update6.sh|bash
```

### 备用节点

**备用节点【香港】：**
```
yum install -y wget && wget -O install.sh http://103.224.251.67:5880/install/install_6.0.sh && sh install.sh
```

**备用节点【美国】：**
```
yum install -y wget && wget -O install.sh http://128.1.164.196:5880/install/install_6.0.sh && sh install.sh
```

**若点击更新后没生效，请尝试重启面板服务：**

```
bt restart
```

##　面板特色功能

- 一键配置服务器环境（LAMP/LNMP）
- 一键安全重启
- 一键创建管理网站、ftp、数据库
- 一键部署SSL证书
- 一键部署源码（discuz、wordpress、dedecms、z-blog、微擎等等）
- 一键配置（定期备份、数据导入、伪静态、301、SSL、子目录、反向代理、切换PHP版本）
- 一键安装常用PHP扩展(fileinfo、intl、opcache、imap、memcache、apc、redis、ioncube、imagick)
- 数据库一键导入导出
- 系统监控（CPU、内存、磁盘IO、网络IO）
- 防火墙端口放行
- SSH开启与关闭及SSH端口更改
- 禁PING开启或关闭
- 方便高效的文件管理器（上传、下载、压缩、解压、查看、编辑等等）
- 计划任务（定期备份、日志切割、shell脚本）
- 软件管理（一键安装、卸载、版本切换）

## 宝塔面板命令大全

### 管理宝塔

宝塔工具箱(包含下列绝大部分功能 直接ssh中执行bt命令 仅限6.x以上版本面板)

```
bt
```

停止

```
/etc/init.d/bt stop
```

启动

```
/etc/init.d/bt start
```

重启

```
/etc/init.d/bt restart
```

卸载

```
/etc/init.d/bt stop && chkconfig --del bt && rm -f /etc/init.d/bt && rm -rf /www/server/panel
```

查看当前面板端口

```
cat /www/server/panel/data/port.pl
```

修改面板端口，如要改成8881（centos 6 系统）

```
echo '8881' > /www/server/panel/data/port.pl && /etc/init.d/bt restart
iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 8881 -j ACCEPT
service iptables save
service iptables restart
```

修改面板端口，如要改成8881（centos 7 系统）

```
echo '8881' > /www/server/panel/data/port.pl && /etc/init.d/bt restart
firewall-cmd --permanent --zone=public --add-port=8881/tcp
firewall-cmd --reload
```

强制修改MySQL管理(root)密码，如要改成123456

```
cd /www/server/panel && python tools.py root 123456
```

修改面板密码，如要改成123456

```
cd /www/server/panel && python tools.py panel 123456
```

查看宝塔日志

```
cat /tmp/panelBoot.pl
```

查看软件安装日志

```
cat /tmp/panelExec.log
```

站点配置文件位置

```
/www/server/panel/vhost
```

删除域名绑定面板

```
rm -f /www/server/panel/data/domain.conf
```

清理登陆限制

```
rm -f /www/server/panel/data/*.login
```

查看面板授权IP

```
cat /www/server/panel/data/limitip.conf
```

关闭访问限制

```
rm -f /www/server/panel/data/limitip.conf
```

查看许可域名

```
cat /www/server/panel/data/domain.conf
```

关闭面板SSL

```
rm -f /www/server/panel/data/ssl.pl && /etc/init.d/bt restart
```

查看面板错误日志

```
cat /tmp/panelBoot
```

查看数据库错误日志

```
cat /www/server/data/*.err
```

站点配置文件目录(nginx)

```
/www/server/panel/vhost/nginx
```

站点配置文件目录(apache)

```
/www/server/panel/vhost/apache
```

站点默认目录

```
/www/wwwroot
```

数据库备份目录

```
/www/backup/database
```

站点备份目录

```
/www/backup/site
```

站点日志

```
/www/wwwlogs
```



### Nginx服务管理

nginx安装目录

```
/www/server/nginx
```

启动

```
/etc/init.d/nginx start
```

停止

```
/etc/init.d/nginx stop
```

重启

```
/etc/init.d/nginx restart
```

启载

```
/etc/init.d/nginx reload
```

nginx配置文件

```
/www/server/nginx/conf/nginx.conf
```



### Apache服务管理

apache安装目录

```
/www/server/httpd
```

启动

```
/etc/init.d/httpd start
```

停止

```
/etc/init.d/httpd stop
```

重启

```
/etc/init.d/httpd restart
```

启载

```
/etc/init.d/httpd reload
```

apache配置文件

```
/www/server/apache/conf/httpd.conf
```



### MySQL服务管理

mysql安装目录

```
/www/server/mysql
```

phpmyadmin安装目录

```
/www/server/phpmyadmin
```

数据存储目录

```
/www/server/data
```

启动

```
/etc/init.d/mysqld start
```

停止

```
/etc/init.d/mysqld stop
```

重启

```
/etc/init.d/mysqld restart
```

启载

```
/etc/init.d/mysqld reload
```

mysql配置文件

```
/etc/my.cnf
```



### FTP服务管理

ftp安装目录

```
/www/server/pure-ftpd
```

启动

```
/etc/init.d/pure-ftpd start
```

停止

```
/etc/init.d/pure-ftpd stop
```

重启

```
/etc/init.d/pure-ftpd restart
```

ftp配置文件

```
/www/server/pure-ftpd/etc/pure-ftpd.conf
```



### PHP服务管理

php安装目录

```
/www/server/php
```

启动(请根据安装PHP版本号做更改，例如：/etc/init.d/php-fpm-54 start)

```
/etc/init.d/php-fpm-{52|53|54|55|56|70|71|72|73|74} start
```

停止(请根据安装PHP版本号做更改，例如：/etc/init.d/php-fpm-54 stop)

```
/etc/init.d/php-fpm-{52|53|54|55|56|70|71|72|73|74} stop
```

重启(请根据安装PHP版本号做更改，例如：/etc/init.d/php-fpm-54 restart)

```
/etc/init.d/php-fpm-{52|53|54|55|56|70|71|72|73|74} restart
```

启载(请根据安装PHP版本号做更改，例如：/etc/init.d/php-fpm-54 reload)

```
/etc/init.d/php-fpm-{52|53|54|55|56|70|71|72|73|74} reload
```

配置文件(请根据安装PHP版本号做更改，例如：/www/server/php/52/etc/php.ini)

```
/www/server/php/{52|53|54|55|56|70|71|72|73|74}/etc/php.ini
```



### Redis服务管理

redis安装目录

```
/www/server/redis
```

启动

```
/etc/init.d/redis start
```

停止

```
/etc/init.d/redis stop
```

redis配置文件

```
/www/server/redis/redis.conf
```



### Memcached服务管理

memcached安装目录

```
/usr/local/memcached
```

启动

```
/etc/init.d/memcached start
```

停止

```
/etc/init.d/memcached stop
```

重启

```
/etc/init.d/memcached restart
```

启载

```
/etc/init.d/memcached r
```
