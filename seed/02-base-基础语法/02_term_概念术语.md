<!--ts-->

- [运行程序、python 解释器](#运行程序python-解释器)
- [变量、数据类型](#变量数据类型)
  - [变量赋值](#变量赋值)
  - [标准数据类型](#标准数据类型)
    - [1. 数字](#1-数字)
      - [1.1 布尔](#11-布尔)
      - [1.2 整数、浮点数](#12-整数浮点数)
        - [运算](#运算)
      - [1.3 复数](#13-复数)
    - [2. 字符串（字符）](#2-字符串字符)
    - [3. 列表](#3-列表)
    - [4. 元组](#4-元组)
    - [5. 集合](#5-集合)
    - [6. 字典](#6-字典)
- [数据类型转换](#数据类型转换)
- [推导式](#推导式)
  - [1. 列表(list)推导式](#1-列表list推导式)
  - [2. 字典(dict)推导式](#2-字典dict推导式)
  - [3. 集合(set)推导式](#3-集合set推导式)
  - [4. 元组(tuple)推导式](#4-元组tuple推导式)

<!-- Added by: edy, at: 2023年 2月 6日 星期一 18时09分06秒 CST -->

<!--te-->

# 运行程序、python 解释器

简单直观的来说，执行的 `python` 命令，就是开启的 python 解释器

[运行 python 命令或脚本](../../run.md)

Python 解释器可不止一种哦，有 `CPython、IPython、Jython、PyPy` 等。

1. 顾名思义，CPython 就是用 C 语言开发的了，是官方标准实现，拥有良好的生态，所以应用也就最为广泛了。
2. 而 IPython 是在 CPython 的基础之上在交互式方面得到增强的解释器 [ipython 官方地址](http://ipython.org/)
3. Jython 是专为 Java 平台设计的 Python 解释器 [jython 官方地址](http://www.jython.org/)，它把 Python 代码编译成 Java 字节码执行。
4. PyPy 是 Python 语言（2.7.13 和 3.5.3）的一种快速、兼容的替代实现 [pypy 官方地址](http://pypy.org/)，以速度快著称。

# 变量、数据类型

什么是变量？

变量是存储在内存中的值。这就意味着在创建变量时会在内存中开辟一个空间。

> 基于变量的数据类型，解释器会分配指定大小的内存，并决定什么数据可以被存储在内存中。

## 变量赋值

等号 `=` 用来给变量赋值。左边：变量，右边：值

```python
#!/usr/bin/python
#coding=utf-8

counter = 100 # 赋值整型变量
miles = 1000.0 # 浮点型
name = "John" # 字符串

print counter  # python3, 使用 print(counter)
print miles
print name
```

例子

```python
# 同时为多个变量赋值
a = b = c = 1
# 以上例子，创建一个整型对象，值为 1，三个变量(a,b,c)被分配到相同的内存空间上

# 为多个对象指定多个变量
a, b, c = 1, 2, "john"
# 以上例子，两个整型对象1和2的分配给变量a和b，字符串对象"john"分配给变量 c
```

## 标准数据类型

基于变量的数据类型，解释器会分配指定大小的内存，并决定什么数据可以被存储在内存中。

Python 有六个标准的数据类型：

- 不可变数据（3 个）: Number（数字）、String（字符串）、Tuple（元组）
- 可变数据（3 个）: List（列表）、Dictionary（字典）、Set（集合）

**很重要一点是类型可以自由地转换，你赋什么值，变量就是什么类型，python 会自动帮你管理**

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-1-type.py)

### 1. 数字

Python3 支持 `int（整数）、float（浮点数）、bool（布尔）、complex（复数）`

数值类型实例

| int    | float      | complex    |
| ------ | ---------- | ---------- |
| 10     | 0.0        | 3.14j      |
| 100    | 15.20      | 45.j       |
| -786   | -21.9      | 9.322e-36j |
| 080    | 32.3e+18   | .876j      |
| -0490  | -90.       | -.6545+0J  |
| -0x260 | -32.54e100 | 3e+26J     |
| 0x69   | 70.2E-12   | 4.53e-7j   |

#### 1.1 布尔

1. python2 中没有布尔类型，它用数字 0 表示 False，用 1 表示 True

2. Python3 中，`bool 是 int 的子类`，True 和 False 可以和数字相加， `True == 1`、`False == 0` 会返回 True，但可以通过 `is` 来判断类型。

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-2-bool.py)

#### 1.2 整数、浮点数

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-3-number.py)

##### 运算

1. 数值的除法包含两个运算符：`/` 返回一个浮点数，`//` 返回一个整数
2. 在混合计算时，Python 会把整型转换成为浮点数

#### 1.3 复数

复数，复数由实数部分和虚数部分构成，可以用 `a + bj`，或者 `complex(a,b)` 表示，复数的实部 a 和虚部 b 都是浮点型。

### 2. 字符串（字符）

字符串用单引号 `'` 或双引号 `"` 括起来，同时使用反斜杠 `\` 转义特殊字符。

1. 反斜杠可以用来**转义**，使用 `r` 可以让反斜杠不发生转义。
2. 字符串可以用 `+` 运算符连接在一起，用 `*` 运算符重复。
3. Python 中的**字符串中的字符不能改变**

> Python 字符串不能被改变。向一个索引位置赋值，比如 `word = 'Python'; word[0] = 'm'` 会导致错误。

字符

Python **没有单独的字符类型**，一个字符就是长度为 1 的字符串

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-4-string.py)

### 3. 列表

列表（list）是写在方括号 `[]` 之间、用 `逗号` 分隔开的元素列表

1. 元素的类型可以不相同
2. 它支持数字，字符串甚至可以包含列表（所谓嵌套）
3. 列表也可以用 `+` 运算符连接在一起，用 `*` 运算符重复。
4. 列表中的**元素可以改变**
5. 元素是**有序的**，是有序的对象集合

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-5-list.py)

### 4. 元组

1. 元组（tuple）与列表类似，元素类型也可以不相同
2. 不同之处在于，元组和与字符串一样，它的**元素不能修改**，但是，**它可以包含可变的对象，比如：list 列表（可以修改列表内的元素）**
3. 元组写在小括号 `()` 里，元素之间用 `逗号` 隔开
4. 元组也可以用 `+` 运算符连接在一起，用 `*` 运算符重复。

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-6-tuple.py)

```python
# 构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

tp3 = ()    # 空元组
print(tp3)

tp4 = (20,)  # 一个元素，需要在元素后添加逗号
print(tp4)
```

### 5. 集合

1. 集合（set）的元素（成员）不会重复
2. 集合中**元素无序**
3. 使用大括号 `{ }` 或者 `set()` 函数创建集合，注意：创建一个**空集合**必须用 `set()` 而不是 `{ }`，因为 `{ }` 是用来创建一个空字典。

应用：

1. 常常用于去重操作
2. 另外进行成员测试操作，可以直接判断 `if 值 in 集合` 是否存在某个元素
3. 进行集合运算，如：`差集（-）、并集（|）、交集（&）、不同时存在（^）`

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-7-set.py)

### 6. 字典

1. 字典是**无序的**对象集合，元素是`键值对`
2. 不同于列表，字典当中的元素是通过键来存取的，而不是通过偏移存取
3. 字典是一种映射类型，字典用 `{ }` 标识，它是一个无序的 `键(key) : 值(value)` 的集合。
4. 键(key) 必须使用**不可变类型**，如：Number（数字）、String（字符串）、Tuple（元组）
5. 在同一个字典中，键(key)必须是**唯一的**

字典类型也有一些内置的函数：

- clear()
- keys()
- values()

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-8-dict.py)

# 数据类型转换

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-9-type-convert.py)

两种：

1. 隐式类型转换 - 自动转换，一般都是数字（如：整数和浮点数运算，此时：较低数据类型（整数）就会转换为较高数据类型（浮点数）以避免数据丢失）
2. 显式类型转换 - 需要使用类型函数来转换，如下：

> 显示类型转换：你只需要将数据类型作为函数名即可，函数返回一个新的对象，表示转换的值。

```bash
# 将x转换为一个整数
int(x [,base])

# 将x转换到一个浮点数
float(x)

# 创建一个复数
complex(real [,imag])

# 将对象 x 转换为字符串
str(x)

# 将对象 x 转换为表达式字符串
repr(x)

# 用来计算在字符串中的有效Python表达式,并返回一个对象
eval(str)

# 将序列 s 转换为一个元组
tuple(s)

# 将序列 s 转换为一个列表
list(s)

# 转换为可变集合
set(s)

# 创建一个字典。d 必须是一个 (key, value)元组序列。
dict(d)

# 转换为不可变集合
frozenset(s)

# 将一个整数转换为一个字符
chr(x)

# 将一个字符转换为它的整数值
ord(x)

# 将一个整数转换为一个十六进制字符串
hex(x)

# 将一个整数转换为一个八进制字符串
oct(x)
```

# 推导式

Python 推导式是一种独特的数据处理方式，**可以从一个数据序列构建另一个新的数据序列的结构体**

1. 列表(list)推导式
2. 字典(dict)推导式
3. 集合(set)推导式
4. 元组(tuple)推导式

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-10-exp.py)

## 1. 列表(list)推导式

格式：

```bash
# [表达式 for 变量 in 列表]
[out_exp_res for out_exp in input_list]

# 或者

# [表达式 for 变量 in 列表 if 条件]
[out_exp_res for out_exp in input_list if condition]

out_exp_res
# 列表生成元素表达式，可以是有返回值的函数，out_exp_res的结果就是列表的元素

for out_exp in input_list
# 迭代 input_list 将 out_exp 传入到 out_exp_res 表达式中

if condition
# 条件语句，可以过滤列表中不符合条件的值
```

## 2. 字典(dict)推导式

格式：

```bash
{ key_expr: value_expr for value in collection }

# 或者

{ key_expr: value_expr for value in collection if condition }

key_expr
# 键(key)表达式，用于生成key的表达式，作为新字典的key

value_expr
# 值(value)表达式，用于生成value的表达式，作为新字典的value

for value in collection
# 迭代 collection 将 value 传入到 key_expr,value_expr 表达式中

if condition
# 条件语句，可以过滤不符合条件的value
```

## 3. 集合(set)推导式

格式：

```bash
{ expression for item in Sequence }

# 或者

{ expression for item in Sequence if conditional }

expression
# 生成新元素的表达式，作为新集合的元素

for item in Sequence
# 迭代 Sequence 将 item 传入到 expression 表达式中

if condition
# 条件语句，可以过滤不符合条件的value
```

## 4. 元组(tuple)推导式

注意，**元组推导式返回的结果是一个生成器对象**

格式：

```bash
(expression for item in Sequence )

# 或者

(expression for item in Sequence if conditional )

# ps: 元组推导式和列表推导式的用法也完全类似
```
