python 常见运行方式：

1. 交互式解释器

不需要创建脚本文件，是通过 Python 解释器的交互模式进来编写代码

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

通过引入解释器可以在命令行中执行 Python 脚本

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

3. 使用 IDE 工具运行

在图形用户界面（GUI）环境下，直接点击按钮就可以
