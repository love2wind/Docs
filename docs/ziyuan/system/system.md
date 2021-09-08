# About Syetem

### office 2016 激活方法

将以下内容复制粘贴到记事本，另存为bat文件，双击即可激活。原理，利用网络上的kms激活服务器激活。

```
@echo off
%1 %2
mshta vbscript:createobject("shell.application").shellexecute("%~s0","goto :runas","","runas",1)(window.close)&goto :eof
:runas
if exist "%ProgramFiles%\Microsoft Office\Office16\ospp.vbs" cd /d "%ProgramFiles%\Microsoft Office\Office16"
if exist "%ProgramFiles(x86)%\Microsoft Office\Office16\ospp.vbs" cd /d "%ProgramFiles(x86)%\Microsoft Office\Office16"
for /f %%x in ('dir /b ..\root\Licenses16\proplusvl*.xrm-ms') do cscript ospp.vbs /inslic:"..\root\Licenses16\%%x" >nul
cscript //nologo ospp.vbs /inpkey:XQNVK-8JYDB-WJ9W3-YJ8YR-WFG99
cscript //nologo ospp.vbs /sethst:kms.03k.org
cscript //nologo ospp.vbs /act
pause
```

亲测成功！

### Windows实用Cmd命令

#### 查看解析IP

```
ping blog.oioweb.cn
```

> blog.oioweb.cn :要查看IP/延迟的域名

#### 查看解析记录

```
nslookup -q=mx qq.com
```

> mx:记录类型 常见的有 A CNAME AAAA MX TXT

#### 清除dns缓存

```
ipconfig /flushdns
```

> dns第一次解析域名以后会缓存在本地，第二次直接使用缓存，为了加快访问速度，但是在域名更换解析IP以后还是缓存的以前IP，就可以使用此命令。

