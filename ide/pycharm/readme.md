<!--ts-->
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

# 环境配置

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

3、接着我们可以选择`New Environment`或`Existing Environment`，建议选择`Existing Environment`，然后根据自己安装 Python 的路径，找到 Python.exe，然后勾选`make avaliable to all projects`，将该 Python 环境应用到所有的项目，点击 OK；

4. 完成上述步骤后，我们就进入了一个页面，这里是我们当前配置的 Python 环境中包含的库信息，点击`apply -> OK`，即可完成我们的 Python 环境配置。
