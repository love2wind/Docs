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

在此记录，以便不时之需。不知道小伙伴们有什么其他的好办法？欢迎留言评论。

