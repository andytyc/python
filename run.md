<!--ts-->

- [解释器](#解释器)
- [多种运行方式](#多种运行方式)
- [IDE](#ide)

<!-- Added by: edy, at: 2023年 3月13日 星期一 14时54分35秒 CST -->

<!--te-->

# 解释器

我们的第一个 Python 程序，打印

```python
# print() 函数的作用是让计算机把你给它的指令结果，显示在屏幕的终端上。
print('Hello Python')
```

它的执行流程如下：

1. 向解释器发出指令，打印 'Hello Python'
2. 解析器把代码解释为计算器能读懂的机器语言
3. 计算机执行完后就打印结果

# 多种运行方式

python 常见运行方式有两种：

1. 交互式解释器

不需要创建脚本文件，是通过 Python 解释器的交互模式进来编写代码，执行 `python` 来启动 Python 解释器

> `>>>` 是 python 提示符，输入命令回车直接查看运行结果

```bash
# root@watrix:/usr/local/lib/python3.8/dist-packages# python3
Python 3.8.10 (default, Nov 14 2022, 12:59:47)
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("hello world")
hello world
>>> exit()
```

2. 运行脚本文件

代码放进 `xx.py` 源代码文件中，作为一个脚本文件，通过引入 python 解释器可以在命令行中执行 Python 脚本

> 检查脚本文件是否有可执行权限

```bash
# root@watrix:/home/watrix/pydo/tmp# python3 hello.py
Hello World!
```

hello.py 如下，

```python
print('Hello World!')
```

> Python3.X 源码文件默认使用 utf-8 编码，所以可以正常解析中文，无需指定 UTF-8 编码。
>
> 但在 python2.x 时，需要头部指定编码的 `coding: UTF-8` 解决当打印的字符串有中文，避免可能出现中文编码错误

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-
print('Hello World!')
```

# IDE

使用 IDE 工具运行，在图形用户界面（GUI）环境下，直接`点击按钮`就可以

> 本质上，其实就是使用的第二种方式（脚本式执行），只是工具按钮封装了此操作而已
