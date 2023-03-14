<!--ts-->

- [介绍](#介绍)
- [参考](#参考)
- [设置](#设置)
  - [python 解释器](#python-解释器)
  - [pycharm 的主题](#pycharm-的主题)
  - [代码的个性化设置](#代码的个性化设置)
    - [1. 字体、字体大小](#1-字体字体大小)
    - [2. 调整注释颜色](#2-调整注释颜色)
  - [文件保存自动格式化](#文件保存自动格式化)
    - [1. 鼠标手动执行](#1-鼠标手动执行)
    - [2. 保存自动格式化](#2-保存自动格式化)
  - [设置作者信息、脚本模板](#设置作者信息脚本模板)

<!-- Added by: edy, at: 2023年 3月14日 星期二 11时28分17秒 CST -->

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

# 设置 Theme 即可，比如：Light 白亮, Darcula 黑色(推荐，对眼睛好)
```

## 代码的个性化设置

不同系统 `mac, windows` 可能一些按钮稍有不同，但大同小异可以理解

[参考](https://developer.aliyun.com/article/590305)

### 1. 字体、字体大小

```bash
# mac
Pycharm -> Preferences | Editor | Font

# windows
File -> Settings ->  Editor | Font

# 选择字体并且调整字体的大小和间距。

# 右侧的Schema可以选择字体配置：
# 这里推荐Menlo或者Monokai

# 可以根据个人习惯来设置，所以字体大小是14，间距1.4
# Size: 14
# Line spacing: 1.4
```

### 2. 调整注释颜色

```bash
# mac
Pycharm -> Preferences | Editor | Color Scheme | Python

# windows
File -> Settings ->  Editor | Color Scheme | Python

# 选择:Line Comment 这个就是注释，右边可以设置颜色，默认是：灰色
```

## 文件保存自动格式化

不同系统 `mac, windows` 可能一些按钮稍有不同，但大同小异可以理解

[参考 1](https://www.fdevops.com/2020/04/05/pycharm-black-auto-save)
[参考 2](https://blog.csdn.net/xhzq1986/article/details/113062353)
[参数 3](https://www.jianshu.com/p/46c0fa679b9f)

好处：

不需要再对着 pep8 标准扣字眼来修改自己代码，减少了组内不必要的讨论，专注于项目功能，代码风格更统一，github 上传代码冲突更少，帮助多人开发协调代码规范，因此大多数公司招聘 python 开发人员时将了解 pep8 规范和懂得使用自动格式化工具列入必备技能。

列举了 python 中的三个自动格式化工具：

- autopep8 - github star 3.5k

- yapf - github star 11k

- black - github star 17.6k

  - [点击 github](https://github.com/psf/black)
  - [使用和基础配置](https://black.readthedocs.io/en/stable/usage_and_configuration/the_basics.html)

使用方式有两种：

- 鼠标手动执行
- 保存自动格式化

### 1. 鼠标手动执行

```bash
# mac
Pycharm -> Prefferences -> Tools -> External Tools

# windows
File -> Settings -> Tools -> External Tools

# 这样我们就进入了配置文件监控设置页面，可以设置文件保存自动格式化

#### 以使用black脚本为力  ####

pip install black

# 添加 + 一个扩展脚本工具，可以以 black 包的方式用python执行如下：

Name: 随便 {如:black}

Program：选择 python 所在的路径
Arguments：-m black $FilePath$
Working directory：$ProjectFileDir$
```

使用时，只需在 py 文件的工作区，右键单击，就能找到格式化插件：`External Tools -> black`

### 2. 保存自动格式化

```bash
# mac
Pycharm -> Prefferences -> Tools -> File Watchers

# windows
File -> Settings -> Tools -> File Watchers

# 这样我们就进入了配置文件监控设置页面，可以设置文件保存自动格式化

#### 以使用black脚本为力  ####

pip install black

# 在刚才 Tools -> File Watchers 页面里，点击 + 添加 Custom 自定义一个模块，直接使用 black 可执行文件

Name: 随便填

File type: Python
Scope: Project Files

Program: 你安装的black的地址 -- 和python在同一个目录下 bin (如果是windows则是scripts) 下的black可执行文件
Arguments: $FilePath$ -l 120 # 每行代码长度 120 (默认：88)
Output paths to refresh: $FilePath$

# 保存，并应用即可 (没生效则重启下pycharm)
```

## 设置作者信息、脚本模板

不同系统 `mac, windows` 可能一些按钮稍有不同，但大同小异可以理解

```bash
# mac
Pycharm -> Preferences | Editor >> File and Code Templates >> Python Script

# windows
File -> Settings ->  Editor >> File and Code Templates >> Python Script

# 可以设置各种xx.py格式的代码文件模版
```

比如，我设置的一个模版是：

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# @Time    : ${DATE}
# @Author  : andytyc
# @Github  : https://github.com/andytyc
# @Project: ${PROJECT_NAME}
# @FileName: ${NAME}.py


def test():
    pass


if __name__ == '__main__':
    test()
    pass
```

- 模版中可用到的规则如下

```bash
（a）shebang行

#!/usr/bin/python3

# 或

#!/usr/bin/env python

（b）预定义的变量要扩展为格式为$ {<variable_name>}的相应值。

可用的预定义文件模板变量为：

$ {PROJECT_NAME} - 当前项目的名称。

$ {NAME} - 在文件创建过程中在“新建文件”对话框中指定的新文件的名称。

$ {USER} - 当前用户的登录名。

$ {DATE} - 当前的系统日期。

$ {TIME} - 当前系统时间。

$ {YEAR} - 今年。

$ {MONTH} - 当月。

$ {DAY} - 当月的当天。

$ {HOUR} - 目前的小时。

$ {MINUTE} - 当前分钟。

$ {PRODUCT_NAME} - 将在其中创建文件的IDE的名称。

$ {MONTH_NAME_SHORT} - 月份名称的前3个字母。 示例：1月，2月等

$ {MONTH_NAME_FULL} - 一个月的全名。 示例：1月，2月等
```
