<!--ts-->

- [介绍](#介绍)
- [标识符](#标识符)
- [代码块（缩进、行、空行）](#代码块缩进行空行)
- [引号](#引号)
- [注释](#注释)
- [多行语句](#多行语句)

<!-- Added by: edy, at: 2023年 2月 3日 星期五 15时36分31秒 CST -->

<!--te-->

# 介绍

python 语法规范是 `PEP8` 规定的

每种语言都有自己的语法，不管是自然语言（英语，中文）还是计算机编程语言。

Python 也不例外，它也有自己的语法规则，然后编辑器或者解析器根据符合语法的程序代码转换成 CPU 能够执行的机器码，然后执行。

# 参考

[参考](https://github.com/walter201230/Python/blob/master/Article/codeSpecification/codeSpecification_first.md)

[参考 (命名规范)](https://github.com/walter201230/Python/blob/master/Article/codeSpecification/codeSpecification_third.md)

[参考 (注释)](https://github.com/walter201230/Python/blob/master/Article/codeSpecification/codeSpecification_second.md)

# 标识符

1. 字母、数字、下划线(`_`)，但不能以数字开头
2. 区分大小写

特殊标识符

> 下划线开头的标识符是有特殊意义的

1. 以单下划线开头（`​_foo`​）的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用 `​from xxx import *`而导入

2. 以双下划线开头的（`​__foo`​）代表类的私有成员

3. 以双下划线开头和结尾的（​`__foo__`​）代表 python 里特殊方法专用的标识，如`​__init__()`​ 代表类的构造函数。

# 代码块（缩进、行、空行）

Python 的代码块不使用大括号`{}`包裹，而是以`缩进和换行`来区分代码块。常见的代码块出现在函数、循环以及逻辑判断等地方。

> 当语句以冒号 : 结尾时，缩进的语句视为代码块
>
> 观赏性好，代码优雅

1. 同一级别的代码块语句必须包含相同的缩进空白数量，错误示范如下：

```python
# if前面有一个空格
 if True:
    print "Answer"
    print "True"
else:
    print "Answer"
    # 没有严格缩进，在执行时报错
  print "False"
```

2. Python 可以同一行显示多条语句，方法是用分号 `;` 分开

> 强烈不建议，这会破坏 python 优雅设计的初衷，代码可读性会下降

```python
######## python2 ########

>>> print 'hello';print 'Python';
hello
Python

######## python3 ########

>>> print("hello");print("Python");
hello
Python
```

3. 空行，严格来说没有意义，不会被 python 解释器翻译，但对于维护代码、可读性来说，空行很重要。

> 根据 PEP8 规范，空行的作用在于分隔两段不同功能或含义的代码

```python
# 类、函数等之间有一个空行隔开

# 函数之间 PEP8 甚至要求两个空行隔开
```

# 引号

单引号 `'`​，双引号 `"` ​，三引号 `​''' """`​ 来表示字符串，引号的开始与结束必须是相同类型的。

```python
#coding=utf-8
word = 'word'
sentence = "这是一个句子"
paragraph = """这是一个段落
包含了多个语句"""
```

# 注释

1. 单行注释采用 ​`#` ​ 开头

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

# 第一个注释
print "Hello, Python!";  # 第二个注释
```

2. 多行注释使用三个单引号 `​'''`​ 或三个双引号 ​`"""​`

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

'''
这是多行注释，使用单引号。
这是多行注释，使用单引号。
这是多行注释，使用单引号。
'''

"""
这是多行注释，使用双引号。
这是多行注释，使用双引号。
这是多行注释，使用双引号。
"""
```

# 多行语句

一个语句放到多行显示（有时一条语句很常时看起来不方便），使用斜杠 `​\`​ 将一行的语句分为多行显示

```python
total = item_one + \
        item_two + \
        item_three

# 语句中包含​[]​,​ {} ​或 ​()​ 括号就不需要使用多行连接符，可直接换行
days = ['Monday', 'Tuesday', 'Wednesday',
        'Thursday', 'Friday']
```
