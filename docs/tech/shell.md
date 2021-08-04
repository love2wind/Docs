# :cool:Linux系统一些不常用命令

### CentOS防火墙firewalld简单命令

- 启动firewall

`systemctlstartfirewalld`

- 停止firewall

`systemctlstopfirewalld`

- 重启firewall

`systemctlrestartfirewalld`

- 禁止开机自启(永久关闭firewall)

`systemctldisablefirewalld.service`

- 查看防火墙状态

`systemctlstatusfirewalld`

- 设置开启自启

`systemctlenablefirewalld`

- 查看自动启动状态

`systemctlis-enabledfirewalld`

?> 更多firewall命令请参考[firewalld常规命令](https://www.cnblogs.com/hubing/p/6058932.html)

### Linux下统计当前文件夹下的文件个数、目录个数

- 查看当前目录下的文件数量（不包含子目录中的文件）

`ls-l|grep“^-“|wc-l`

- 查看当前目录下的文件数量（包含子目录中的文件）注意：R，代表子目录

`ls-lR|grep“^-“|wc-l`

- 查看当前目录下的文件夹目录个数（不包含子目录中的目录），如果需要查看子目录的，加上R

`ls-l|grep“^d”|wc-l`

- 查询当前路径下的指定前缀名的目录下的所有文件数量
例如：统计所有以“20161124”开头的目录下的全部文件数量

`ls-lR20161124*/|grep“^-“|wc-l`

?> grep“^d”表示目录，”^-“表示文件，wc-l表示统计输出信息的行数，因为经过前面的过滤已经只剩下普通文件，一个目录或文件对应一行，所以统计的信息的行数也就是目录或文件的个数

### 查找最占资源的程序

- 找出占用内存资源最多的前10个进程

`ps-auxf|sort-nr-k4|head-10`

- 找出占用CPU资源最多的前10个进程

`ps-auxf|sort-nr-k3|head-10`

找到目标程序的**pid**，然后**kill**就可以了(前提知道风险)

### docker常用基本命令

dockerimages  #查看镜像
dockerps  #查看当前已经运行的容器
dockerps-a  #查看当前所有的容器
dockerps-a-q  #只显示当前运行的容器的ID号
docker rm -f +前4位容器ID号
dockerrm-f$(dockerps-a-q)  #删除当前运行的所有容器

dockersystemprune-a  #回收垃圾,执行这个，才会从硬盘彻底清除



dockerpull  #下载镜像dockerpullhub.c.163.com/public/centos:6.7-tools
dockerrun  #从镜像运行为容器
dockerstart/stop  #容器启动停止
docker rmi +别名或ID号   #Docker 镜像的删除
dockersimages-a-q  #显示镜像所有的ID号
dockerrmi-f$(dockerimages-a-q)  #强制删除所有镜像

**单一容器管理命令：**

dockerps–no-trunc  #查看容器详细信息
dockerstop/startCONTAINERID  #通过容器id启动/停止
dockerrun–restart=always  #容器的自动启动
dockerstart/stopMywordPress  #通过容器别名启动/停止
dockerinspectMywordPress  #查看容器所有基本信息
dockerlogsMywordPress  #查看容器日志
dockerstatsMywordPress  #查看容器所占用的系统资源
dockerexec 容器名 容器内执行的命令  #容器执行命令
docker exec -it 容器名 /bin/bash #登陆容器的bash

### Linux四合一加速脚本(BBR、锐速、BBRPlus)

`wget-N–no-check-certificate“https://github.000060000.xyz/tcp.sh”&&chmod+xtcp.sh&&./tcp.sh`