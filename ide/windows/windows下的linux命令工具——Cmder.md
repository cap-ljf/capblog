对于很多开发者来说，linux虽然用得不太熟悉，但是linux下的很多命令已经功能都是必不可少的。例如curl、ssh、vim，在日常开发运维工作中都是使用频率很高的工具。本文将介绍一款windows下的linux命令行集成工具**Cmder**。

## 1.Cmder介绍
Cmder官网：[https://cmder.net/](https://cmder.net/)
![image.png](0)
官网介绍：
*Cmder is a software package created out of pure frustration over the absence of nice console emulators on Windows. It is based on amazing software, and spiced up with the Monokai color scheme and a custom prompt layout, looking sexy from the start.*
Cmder是一个软件包，诞生的原因是因为windows下缺少好用的控制台模拟器。它基于令人惊叹的软件，并采用Monokai配色方案和自定义快速布局，从一开始就看起来很性感。

## 2.启动Cmder
软件解压之后直接双击`Cmder.exe`文件即可运行。但是每次都要这样打开很麻烦，你也可以选择把它固定到任务栏，但是每次打开之后进入的目录都是Cmder的解压目录。这里介绍两种方法方便启动Cmder：

### 2.1 把cmder添加到环境变量Path
首先打开 控制面板->系统安全->系统->高级系统设置->环境变量->系统变量：
![image.png](1)
把Cmder的解压目录 添加到Path变量后，保存之后，使用`win + r`命令，输入Cmder即可启动，进入的目录是用户目录。
![image.png](2)

### 2.2 添加cmder到右键菜单
我们可以知道windows下安装完git后一般会将Git Bash添加到右键菜单里，这样我们可以在任意目录里右键都能看到Git Bash，从哪个目录打开的bash，路径都是当前目录。所以可以把cmder添加到右键菜单，从任意目录打开cmder进入的路径都是当前目录。实际上上一步的把 cmder 加到环境变量就是为此服务的, 在管理员权限的终端输入以下语句:
``` 
Cmder.exe /REGISTER ALL
```
![image.png](3)


## 常用快捷键

**Tab manipulation**
`` Ctrl + ` ``: 全局切换任务栏
`Win + Alt + p`: 偏好设置（或者右键Tab标题）
`Ctrl + t`: 打开一个新Tab（需选择cmd类型，例如管理员？可以设置默认打开tab的shell类型）
`Ctrl + w`: 关闭当前Tab
`Shift + Alt + number`: 快速打开一个Tab
	1.CMD
	2.PowerShell
`Alt + Enter`: 全屏/退出全屏

**Shell**
`Ctrl + Alt + u`: 回退到上一个目录
`Ctrl + r`: 搜索历史命令
`Shift + mouse / 左键选择`: 复制文本
`Right click / Ctrl + Shift + v`: 粘贴文本

参考文献：
> 1.[Win下必备神器之Cmder](https://www.jeffjade.com/2016/01/13/2016-01-13-windows-software-cmder/)
> 2.[https://cmder.net/](https://cmder.net/)