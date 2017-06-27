
## bat 方法

如果你的目录中包含了`NppShell_03.dll, NppShell_04.dll, NppShell_05.dll`，不同的版本里面的这个文件名称不一样。你也可以到网上下载一个这样的dll文件，如果有这样的文件，把下面的代码用记事本保存为“Notepad++右键菜单添加or卸载工具.bat”，放到Notepad++的安装目录下面或者NppShell_04.dll在相同的目录下面，保存为bat文件执行即可。

### 代码如下：

```js
@Echo Off
title Notepad++右键菜单添加or卸载工具

SetLocal EnableDelayedExpansion
echo 1.添加Notepad++右键菜单
echo ------------------------
echo 2.卸载Notepad++右键菜单
echo ------------------------

Set /p u=请输入数字并按Enter确定：

If "%u%"=="1" Goto regnp++
If "%u%"=="2" Goto unregnp++

:regnp++
regsvr32   NppShell_04.dll
exit

:unregnp++
regsvr32  /u NppShell_04.dll
exit

```