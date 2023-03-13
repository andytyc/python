<!--ts-->

- [介绍](#介绍)
- [参考](#参考)
- [设置](#设置)
  - [python 解释器](#python-解释器)
  - [pycharm 的主题](#pycharm-的主题)
  - [文件保存自动格式化](#文件保存自动格式化)
  - [代码的个性化设置](#代码的个性化设置)

<!-- Added by: edy, at: 2023年 3月13日 星期一 20时10分49秒 CST -->

<!--te-->

# 介绍

PyCharm 是由 JetBrains 打造的一款 Python IDE，支持 macOS、 Windows、 Linux 系统。

PyCharm 功能: 调试、语法高亮、Project 管理、代码跳转、智能提示、自动完成、单元测试、版本控制……

1. Professional（专业版，收费）：完整的功能，可试用 30 天。（可破解，最省事的是淘宝几块钱 jetbrains 全家桶）

> 专业版(professional)，可以使用 html,js,sql 等，一般开发者编写代码，都使用专业版

2. Community（社区版，免费）：阉割版的专业版。

# 参考

- [PyCharm 下载地址](https://www.jetbrains.com/pycharm/download/)
- [PyCharm 安装地址](http://www.runoob.com/w3cnote/pycharm-windows-install.html)

# 设置

[参考](https://developer.aliyun.com/article/531180)

## python 解释器

不同系统 `mac, windows` 可能一些按钮稍有不同，但大同小异可以理解

1. 这样我们就进入了配置 Python 环境的界面

```bash
# mac
Pycharm -> Prefferences -> Project -> Project Interpreter

# windows
File -> Settings -> Project -> Project Interpreter

# 这样我们就进入了配置Python环境的界面
```

2. 点击小齿轮，在弹出的选项中点击`Show All`，然后在弹出的窗口中点击`+`号，进入配置页面；

3、接着我们可以选择`New Environment`或`Existing Environment`，建议选择`Existing Environment`，然后根据自己安装 `Python` 的路径，找到 Python.exe，然后勾选`make avaliable to all projects`，将该 Python 环境应用到所有的项目，点击 OK；

4. 完成上述步骤后，我们就进入了一个页面，这里是我们当前配置的 Python 环境中包含的库信息，点击`apply -> OK`，即可完成我们的 Python 环境配置。

## pycharm 的主题

不同系统 `mac, windows` 可能一些按钮稍有不同，但大同小异可以理解

```bash
# mac
Pycharm -> Prefferences ->  Appearance & Behavior -> Appearance

# windows
File -> Settings -> Appearance & Behavior -> Appearance

# 设置 Theme 即可，比如：Light 白亮, Darcula 黑色
```

## 文件保存自动格式化

不同系统 `mac, windows` 可能一些按钮稍有不同，但大同小异可以理解

[参考](https://www.fdevops.com/2020/04/05/pycharm-black-auto-save)

```bash
# mac
Pycharm -> Prefferences -> Tools -> File Watchers

# windows
File -> Settings -> Tools -> File Watchers

# 这样我们就进入了配置文件监控设置页面，可以设置文件保存自动格式化

#### 以使用black脚本为力  ####

pip install black

# 在刚才 Tools -> File Watchers 页面里，点击 + 添加 Custom 自定义一个模块

Name: 随便填

File type: Python
Scope: Project Files

Program: 你安装的black的地址 (和python在同一个目录下，bin 如果是windows则是scripts)
Arguments: $FilePath$ -l 120 # 每行代码长度 120
Output paths to refresh: $FilePath$

# 保存，并应用即可

# 可能还需要重启
```

## 代码的个性化设置

不同系统 `mac, windows` 可能一些按钮稍有不同，但大同小异可以理解

```bash
# mac
Pycharm -> Preferences | Editor | Font

# windows
File -> Settings ->  Editor | Font

# 可以设置代码字体大小
```
