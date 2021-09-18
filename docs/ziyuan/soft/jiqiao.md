## 删除百度网盘等残留图标

### 1/ 修改注册表

`Ctrl+R` 打开运行窗口，输入 `regedit`打开注册表编辑器

找到下列键值

`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\`

把下面的对应目录删除即可

- **百度网盘：** ` {679F137C-3162-45da-BE3C-2F9C3D093F64}`
- **360云盘：** `{01249E9F-88FF-45d5-82DB-A1BEE06E123C}`
- **爱奇艺：** `{BA16CE0E-728C-4FC9-11E5-D0B35B384552}`
- **PPS：** `{CF3CDEFB-31BE-43AE-B064-B9C62C883259}`
- **WPS网盘：** `{5FCD4425-CA3A-48F4-A57C-B8A75C32ACB1}`

### 2/ 软件设置

如果没有卸载软件的时候，可以直接在软件设置里找到类似`在我的电脑中显示WPS网盘入口`的设置项，取消勾选就可以了，其他软件都类似。

![image-20210918140213485](https://i.loli.net/2021/09/18/mPGVnsE2UZ59Mvc.png)