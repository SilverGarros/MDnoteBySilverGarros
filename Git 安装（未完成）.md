# Git 安装教程

## 一、前言

**Git** 是目前世界上最先进的分布式版本控制系统。
工作流程

![img](assets/v2-3bc9d5f2c49a713c776e69676d7d56c5_720w.png)

Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库

## 二、安装教程

### 2.1 在 Windows 上安装 Git 

#### 2.1.1下载Git For Windows (msysGit)

在 Windows 上安装 Git 也有几种安装方法。 
官方版本可以在 Git 官方网站下载。 打开 https://git-scm.com/download/win，下载会自动开始。 要注意这是一个名为 Git for Windows 的项目（也叫做 msysGit），和 Git 是分别独立的项目；更多信息请访问 http://msysgit.github.io/。

另一个简单的方法是安装 **GitHub Desktop**。 该安装程序包含图形化和命令行版本的 Git。 它也能支持 Powershell，提供了稳定的凭证缓存和健全的换行设置。 稍后我们会对这方面有更多了解，现在只要一句话就够了，这些都是你所需要的。 你可以在 GitHub for Windows 网站下载，网址为 [GitHub Desktop 网站](https://desktop.github.com/)。

![image-20240107155035563](assets/image-20240107155035563.png)

如果因为网络问题无法下载或者下载速度过慢，可以选择使用阿里镜像网站[CNPM Binaries Mirror (npmmirror.com)](https://registry.npmmirror.com/binary.html?path=git-for-windows/)进行下载。

![image-20240107155845404](assets/image-20240107155845404.png)

最新版的请翻到网站最下面，点击你要下载的版本
在新打开的下载页面根据系统版本下载 exe 文件。

![image-20240107160043062](assets/image-20240107160043062.png)

#### 2.2.2 Git 的安装

安装演示的版本是 `Git-2.43.0-64-bit.exe`

###### 2.2.2.1 使用许可声明

双击下载后的 Git-2.43.0-64-bit.exe ，开始安装，界面展示了Git 使用的 GPL 协议内容，点击[Next] 
![image-20240107160714540](assets/image-20240107160714540.png)

###### 2.2.2.2 选择安装目录

![image-20240107160848087](assets/image-20240107160848087.png)

###### 2.2.2.3 选择安装组件

根据需要选择勾选，点击 [next]。

![image-20240107160942080](assets/image-20240107160942080.png)
![image-20240107161053893](assets/image-20240107161053893.png)
2.2.2.4 选择开始菜单文件夹

方框内 Git 可改为其他名字，也可点击 “`Browse...`” 选择其他文件夹或者给"`Don't create a Start Menu folder`" 打勾不要文件夹，点击 [next] 。
![image-20240107161235736](assets/image-20240107161235736.png)
安装成功后在开始菜单里的图如下：

###### 2.2.2.4 选择 Git 默认编辑器

Git 安装程序里面内置了多种编辑器，如`Vim`、`Atom`、`Notepad`、`Notepad++`、`Sublime Text`、`Visual Studio Code`，默认的是 Vim ，选择 Vim 后可以直接进行到下一步。
如果选其他编辑器，则还需要去其官网安装后进行环境变量配置才能进行下一步。
![image-20240107161633547](assets/image-20240107161633547.png)

由于 `Vim`极高的学习成本，如果你不想要使用 `Vim` 当默认编辑器，推荐使用`Sublime Text` 。

首选点击蓝色字体"Sublime Text" 去官网下载安装之后才能进行下一步。

![image-20240107161727679](assets/image-20240107161727679.png)

![image-20240107162117302](assets/image-20240107162117302.png)

点击蓝色按钮 DOWNLOAD FOR WINDOWS 开始下载打开setup.exe，点击[Next]。
![image-20240107162238645](assets/image-20240107162238645.png)
点击Install完成安装
![image-20240107162310778](assets/image-20240107162310778.png)
接下来要找到Sublime Text 的完整路径添加到系统变量后重启电脑，然后重新开始Git 的安装
默认路径为`D:\ProgramApplication\Sublime Text\sublime text.exe`

###### 2.2.2.5 命名初始化新仓库（项目）的主干名

第一种是让 Git 自己选择，名字是 `master` ，但是未来也有可能会改为其他名字；第二种是我们自行决定，默认是 `main`，当然，你也可以改为其他的名字。一般默认第一种，点击 [next] 。
第二种进行自命名，由于国外种族问题，导致部分人认为 master 不尊重黑人，呼吁改为 main ，目前很多团队已经重命名默认主干名为 main 。

###### 2.2.2.6 调整Path环境变量

第一种是仅从 Git Bash 使用 Git。这个的意思就是你只能通过 Git 安装后的 Git Bash 来使用 Git ，其他的什么命令提示符啊等第三方软件都不行。

第二种是从命令行以及第三方软件进行 Git。这个就是在第一种基础上进行第三方支持，你将能够从 Git Bash，命令提示符(cmd) 和 Windows PowerShell 以及可以从 Windows 系统环境变量中寻找 Git 的任何第三方软件中使用 Git。推荐使用这个。

第三种是从命令提示符使用 Git 和可选的 Unix 工具。选择这种将覆盖 Windows 工具，如 “ find 和 sort ”。只有在了解其含义后才使用此选项。
![image-20240107164038679](assets/image-20240107164038679.png)

##### 2.2.2.7 选择 SSH 执行文件

![image-20240107164120740](assets/image-20240107164120740.png)

###### 2.2.2.8 选择 HTTPS 后端传输

![image-20240107164208165](assets/image-20240107164208165.png)

###### 2.2.2.9 配置行尾符号转换

![image-20240107164244110](assets/image-20240107164244110.png)

###### 2.2.2.10 配置终端模拟器以与 Git Bash 一起使用

![image-20240107164346744](assets/image-20240107164346744.png)

###### 2.2.2.11 选择默认 "git pull" 行为

![image-20240107164436169](assets/image-20240107164436169.png)

###### 2.2.2.12 选择凭证帮助程序

![image-20240107164524785](assets/image-20240107164524785.png)

###### 2.2.2.13 配置额外选项

实验性功能，可能会遇到一些小错误，不建议开启，点击[install]进行安装。

![image-20240107164617815](assets/image-20240107164617815.png)
安装......等待安装完成
![image-20240107164711395](assets/image-20240107164711395.png)

安装完成![image-20240107164808438](assets/image-20240107164808438.png)

 
