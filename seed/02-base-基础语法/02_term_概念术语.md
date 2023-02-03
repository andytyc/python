<!--ts-->

- [import 模块](#import-模块)
- [变量、数据类型](#变量数据类型)
  - [变量赋值](#变量赋值)
  - [标准数据类型](#标准数据类型)
    - [1. 数字](#1-数字)
      - [1.1 布尔](#11-布尔)
      - [1.2 整数、浮点数](#12-整数浮点数)
        - [运算](#运算)
      - [1.3 复数](#13-复数)

<!-- Added by: edy, at: 2023年 2月 3日 星期五 18时57分25秒 CST -->

<!--te-->

# import 模块

`xxx.py` 一个 py 源代码文件就是一个模块，可通过文件路径进行导入

```python

```

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

- 不可变数据（3 个）: Number（数字）、String（字符串）、Tuple（元组）；
- 可变数据（3 个）: List（列表）、Dictionary（字典）、Set（集合）。

**很重要一点是类型可以自由地转换，你赋什么值，变量就是什么类型，python 会自动帮你管理**

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-1.py)

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

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-2.py)

#### 1.2 整数、浮点数

##### 运算

1. 数值的除法包含两个运算符：`/` 返回一个浮点数，`//` 返回一个整数
2. 在混合计算时，Python 会把整型转换成为浮点数

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-3.py)

#### 1.3 复数

复数，复数由实数部分和虚数部分构成，可以用 `a + bj`，或者 `complex(a,b)` 表示，复数的实部 a 和虚部 b 都是浮点型。
