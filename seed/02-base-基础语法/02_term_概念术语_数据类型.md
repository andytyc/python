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

Python 有**六个标准**的数据类型：

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

### 2. 字符串

字符串用单引号 `'` 或双引号 `"` 括起来，同时使用反斜杠 `\` 转义特殊字符。

1. 反斜杠可以用来**转义**，使用 `r` 可以让反斜杠不发生转义。
2. 字符串可以用 `+` 运算符连接在一起，用 `*` 运算符重复。
3. Python 中的**字符串中的字符不能改变**

> Python 字符串不能被改变。向一个索引位置赋值，比如 `word = 'Python'; word[0] = 'm'` 会导致错误。

#### 2.1 字符

Python **没有单独的字符类型**，一个字符就是长度为 1 的字符串

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-4-string.py)

### 3. 列表

列表（list）是写在方括号 `[]` 之间、用 `逗号` 分隔开的元素列表

1. 元素的类型可以不相同
2. 它支持数字，字符串甚至可以包含列表（所谓嵌套）
3. 列表也可以用 `+` 运算符连接在一起，用 `*` 运算符重复。
4. 列表中的**元素可以改变**
5. 元素是**有序的**，是有序的对象集合

[code 1](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-5-list.py)
[code 2](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-5-list-case-1.py)

[参考](https://github.com/walter201230/Python/blob/master/Article/PythonBasis/python3/List.md)

#### 3.1 怎么删除 List（列表） 里面的元素

例子中我们就需要在列表中，把一个名字去掉。

这时候使用 del 语句来删除列表的的元素

```python
name = ['一点水', '两点水', '三点水', '四点水', '五点水']

print(name)

# 使用 del 语句来删除列表的的元素
del name[3]
print(name)
```

#### 3.2 List（列表）运算符

列表对 `+` 和 `*` 的操作符与字符串相似。`+` 号用于组合列表，`*` 号用于重复列表。

| Python 表达式                | 结果                         | 描述                 |
| ---------------------------- | ---------------------------- | -------------------- |
| len([1, 2, 3])               | 3                            | 计算元素个数         |
| [1, 2, 3] + [4, 5, 6]        | [1, 2, 3, 4, 5, 6]           | 组合                 |
| ['Hi!'] \* 4                 | ['Hi!', 'Hi!', 'Hi!', 'Hi!'] | 复制                 |
| 3 in [1, 2, 3]               | True                         | 元素是否存在于列表中 |
| for x in [1, 2, 3]: print x, | 1 2 3                        | 迭代                 |

#### 3.3 List （列表）函数&方法

| 函数&方法               | 描述                                                               |
| ----------------------- | ------------------------------------------------------------------ |
| len(list)               | 列表元素个数                                                       |
| max(list)               | 返回列表元素最大值                                                 |
| min(list)               | 返回列表元素最小值                                                 |
| list(seq)               | 将元组转换为列表                                                   |
| list.append(obj)        | 在列表末尾添加新的对象                                             |
| list.count(obj)         | 统计某个元素在列表中出现的次数                                     |
| list.extend(seq)        | 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| list.index(obj)         | 从列表中找出某个值第一个匹配项的索引位置                           |
| list.insert(index, obj) | 将对象插入列表                                                     |
| list.pop(obj=list[-1])  | 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值       |
| list.remove(obj)        | 移除列表中的一个元素（参数是列表中元素），并且不返回任何值         |
| list.reverse()          | 反向列表中元素                                                     |
| list.sort([func])       | 对原列表进行排序                                                   |

### 4. 元组

1. 元组（tuple）与列表类似，元素类型也可以不相同
2. 不同之处在于，**元组和与字符串一样，它的元素不能修改**，但是，**它可以包含可变的对象，比如：list 列表（可以修改列表内的元素）**
3. 元组写在小括号 `()` 里，元素之间用 `逗号` 隔开
4. 元组也可以用 `+` 运算符连接在一起，用 `*` 运算符重复。

[code 1](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-6-tuple.py)
[code 2](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-6-tuple-case-1.py)

[参考](https://github.com/walter201230/Python/blob/master/Article/PythonBasis/python3/tuple.md)

```python
# 构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

tp3 = ()    # 空元组
print(tp3)

tp4 = (20,)  # 一个元素，需要在元素后添加逗号
print(tp4)
```

- 特点

tuple 一旦初始化就不能修改。 也就是说元组（tuple）是不可变的，那么不可变是指什么意思呢？

元组（tuple） 不可变是指当你创建了 tuple 时候，它就不能改变了，也就是说它也没有 append()，insert() 这样的方法，但它也有获取某个索引值的方法，但是不能赋值。

那么为什么要有 tuple 呢？

那是因为 tuple 是不可变的，所以代码更安全。所以建议能用 tuple 代替 list 就尽量用 tuple 。

- 初始化

```python
# 元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可
tuple1=('两点水','twowter','liangdianshui',123,456)
# 不加()时，也可以如下这样，类似多个变量声明赋值，其实就是元组的解包/组包
tuple2='两点水','twowter','liangdianshui',123,456

# 创建空元组
tuple3=()

# 元组中只包含一个元素时，需要在元素后面添加逗号
tuple4=(123,)

# 如果不加逗号，创建出来的就不是 元组（tuple），而是指 123 这个数了。
# 这是因为括号 () 既可以表示元组（tuple），又可以表示数学公式中的小括号，这就产生了歧义。
```

#### 4.1 修改元组 （tuple）

可能看到这个小标题有人会疑问，上面不是花了一大段来说 tuple 是不可变的吗？

这里怎么又来修改 tuple （元组） 了。

那是因为元组中的元素值是不允许修改的，但我们可以对元组进行连接组合，还有通过修改其他列表的值从而影响 tuple 的值。

具体看下面的这个例子：

```python
#-*-coding:utf-8-*-

list1=[123,456]
tuple1=('两点水','twowater','liangdianshui',list1)
print(tuple1)
list1[0]=789
list1[1]=100
print(tuple1)

# 输出的结果：
# ('两点水', 'twowater', 'liangdianshui', [123, 456])
# ('两点水', 'twowater', 'liangdianshui', [789, 100])
```

可以看到，两次输出的 tuple 值是变了的。我们看看 tuple1 的存储是怎样的。

- tuple1 有四个元素，最后一个元素是一个 List ，List 列表里有两个元素。
- 当我们把 List 列表中的两个元素 124 和 456 修改为 789 和 100 的时候，从输出来的 tuple1 的值来看，好像确实是改变了。
- 但其实变的不是 tuple 的元素，而是 list 的元素。
- tuple 一开始指向的 list 并没有改成别的 list，所以，tuple **所谓的“不变”是说，tuple 的每个元素，指向永远不变**。注意是 tupe1 中的第四个元素还是指向原来的 list ，是没有变的，我们修改的只是列表 List 里面的元素。

#### 4.2 删除 tuple （元组）

tuple 元组中的元素值是不允许删除的，但我们可以使用 del 语句来删除整个元组

```python
#-*-coding:utf-8-*-

tuple1=('两点水','twowter','liangdianshui',[123,456])
print(tuple1)
del tuple1
```

#### 4.3 tuple （元组）运算符

与字符串一样，元组之间可以使用 `+` 号和 `*` 号进行运算。这就意味着他们可以组合和复制，运算后会生成一个新的元组。

| Python 表达式                | 结果                         | 描述         |
| ---------------------------- | ---------------------------- | ------------ |
| len((1, 2, 3))               | 3                            | 计算元素个数 |
| (1, 2, 3) + (4, 5, 6)        | (1, 2, 3, 4, 5, 6)           | 连接         |
| ('Hi!',) \* 4                | ('Hi!', 'Hi!', 'Hi!', 'Hi!') | 复制         |
| 3 in (1, 2, 3)               | True                         | 元素是否存在 |
| for x in (1, 2, 3): print(x) | 1 2 3                        | 迭代         |

#### 4.4 元组内置函数

| 方法       | 描述                 |
| ---------- | -------------------- |
| len(tuple) | 计算元组元素个数     |
| max(tuple) | 返回元组中元素最大值 |
| min(tuple) | 返回元组中元素最小值 |
| tuple(seq) | 将列表转换为元组     |

### 5. 集合

1. 集合（set）的元素（成员）不会重复「自动去重功能」
2. 集合中**元素无序**
3. 使用大括号 `{ }` 或者 `set()` 函数创建集合，注意：创建一个**空集合**必须用 `set()` 而不是 `{ }`，因为 `{ }` 是用来创建一个空字典。

应用：

1. 常常用于去重操作
2. 另外进行成员测试操作，可以直接判断 `if 值 in 集合` 是否存在某个元素
3. 进行集合运算，如：`差集（-）、并集（|）、交集（&）、不同时存在（^）`

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-7-set.py)

[参考](https://github.com/walter201230/Python/blob/master/Article/PythonBasis/python4/Set.md)

python 的 set 和其他语言类似, 是一个无序不重复元素集, 基本功能包括`关系测试(并集、交集、差集)`和`消除重复`元素。

set 和 dict 类似，但是 set 不存储 value 值的。

- 初始化

创建一个 set，需要提供一个 list 作为输入集合

```python
set1=set([123,456,789])
print(set1)

# 输出结果：
# {456, 123, 789}
```

传入的参数 [123,456,789] 是一个 list，而显示的 {456, 123, 789} 只是告诉你这个 set 内部有 456, 123, 789 这 3 个元素，显示的顺序跟你参数中的 list 里的元素的顺序是不一致的，这也说明了 set 是无序的。

还有一点，我们观察到输出的结果是在大括号中的，经过之前的学习，可以知道，tuple (元组) 使用小括号，list (列表) 使用方括号, dict (字典) 使用的是大括号，dict 也是无序的，只不过 dict 保存的是 key-value 键值对值，而 set 可以理解为只保存 key 值。

回忆一下，在 dict （字典） 中创建时，有重复的 key ，会被后面的 key-value 值覆盖的，而 重复元素在 set 中自动被过滤的。

```python
set1=set([123,456,789,123,123])
print(set1)

# 输出的结果：
# {456, 123, 789}
```

#### 5.1 set 添加元素

通过 add(key) 方法可以添加元素到 set 中，可以重复添加，但不会有效果

```python
set1=set([123,456,789])
print(set1)
set1.add(100)
print(set1)
set1.add(100)
print(set1)
```

输出结果：

```
{456, 123, 789}
{456, 123, 100, 789}
{456, 123, 100, 789}
```

#### 5.2 set 删除元素

通过 remove(key) 方法可以删除 set 中的元素

```python
set1=set([123,456,789])
print(set1)
set1.remove(456)
print(set1)
```

输出的结果：

```
{456, 123, 789}
{123, 789}
```

#### 5.3 set 的运用

因为 set 是一个无序不重复元素集，因此，两个 set 可以做数学意义上的 union(并集), intersection(交集), difference(差集) 等操作。

[![set集合运算](https://camo.githubusercontent.com/b05947464ef479a005b85cd3bb24f1b66c79d04e96e97e6790e2a2b229885fd5/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f323133363931382d373333623164313037316637373262643f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](https://camo.githubusercontent.com/b05947464ef479a005b85cd3bb24f1b66c79d04e96e97e6790e2a2b229885fd5/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f323133363931382d373333623164313037316637373262643f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)

例子：

```python
set1=set('hello')
set2=set(['p','y','y','h','o','n'])
print(set1)
print(set2)

# 交集 (求两个 set 集合中相同的元素)
set3=set1 & set2
print('\n交集 set3:')
print(set3)

# 并集 （合并两个 set 集合的元素并去除重复的值）
set4=set1 | set2
print('\n并集 set4:')
print(set4)

# 差集
set5=set1 - set2
set6=set2 - set1
print('\n差集 set5:')
print(set5)
print('\n差集 set6:')
print( set6)

# 去除海量列表里重复元素，用 hash 来解决也行，只不过感觉在性能上不是很高，用 set 解决还是很不错的
list1 = [111,222,333,444,111,222,333,444,555,666]
set7=set(list1)
print('\n去除列表里重复元素 set7:')
print(set7)
```

运行的结果：

```
{'h', 'l', 'e', 'o'}
{'h', 'n', 'o', 'y', 'p'}

交集 set3:
{'h', 'o'}

并集 set4:
{'h', 'p', 'n', 'e', 'o', 'y', 'l'}

差集 set5:
{'l', 'e'}

差集 set6:
{'p', 'y', 'n'}

去除列表里重复元素 set7:
{555, 333, 111, 666, 444, 222}
```

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

[参考](https://github.com/walter201230/Python/blob/master/Article/PythonBasis/python4/Dict.md)

- 什么是字典？为什么选择？

在讲列表（list）的时候，我们用了列表（list） 来存储用户的姓名。

```python
name = ['一点水', '两点水', '三点水', '四点水', '五点水']
```

那么如果我们为了方便联系这些童鞋，要把电话号码也添加进去，该怎么做呢？

用 list 可以这样子解决：

```python
name = [['一点水', '131456780001'], ['两点水', '131456780002'], ['三点水', '131456780003'], ['四点水', '131456780004'], ['五点水', '131456780005']]
```

如果用列表来存储这些，列表越长，我们查找起来耗时就越长。

这时候就可以用 dict （字典）来表示了，Python 内置了 字典（dict），dict 全称 dictionary，如果学过 Java ，字典就相当于 JAVA 中的 map，使用键-值（key-value）存储，具有极快的查找速度。

```python
name = {'一点水': '131456780001', '两点水': '131456780002', '三点水': '131456780003', '四点水': '131456780004', '五点水': '131456780005'}
```

- 初始化

字典是另一种可变容器模型，且可存储任意类型对象。

字典的每个键值(key=>value)对用冒号(:)分割，每个对之间用逗号(,)分割，整个字典包括在花括号({})中 ,格式如下所示：

```python
dict = {key1 : value1, key2 : value2 }

# 注意：键必须是唯一的，但值则不必。值可以取任何数据类型，但键必须是不可变的。

# 创建 dict（字典）实例：
dict1={'liangdianshui':'111111', 'twowater':'222222', '两点水':'333333'}
dict2={'abc':1234, 1234:'abc'}
```

#### 6.1 访问 dict （字典）

我们知道了怎么创建列表了，回归到一开始提出到的问题，为什么使用字典能让我们很快的找出某个童鞋的电话呢？

```python
name = {'一点水': '131456780001', '两点水': '131456780002', '三点水': '131456780003', '四点水': '131456780004', '五点水': '131456780005'}

print(name['两点水'])
```

输出的结果：

```
131456780002
```

可以看到，如果你知道某个人的名字，也就是 key 值， 就能很快的查找到他对应的电话号码，也就是 Value 。

这里需要注意的一点是：如果字典中没有这个键，是会报错的。

#### 6.2 修改 dict （字典）

向字典添加新内容的方法是增加新的键值对，修改或删除已有键值对

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333'}
print(dict1)

# 新增一个键值对
dict1['jack']='444444'
print(dict1)

# 修改键值对
dict1['liangdianshui']='555555'
print(dict1)
```

输出的结果：

```
{'liangdianshui': '111111', 'twowater': '222222', '两点水': '333333'}
{'liangdianshui': '111111', 'twowater': '222222', '两点水': '333333', 'jack': '444444'}
{'liangdianshui': '555555', 'twowater': '222222', '两点水': '333333', 'jack': '444444'}
```

#### 6.3 删除 dict （字典）

通过 `del` 可以删除 dict （字典）中的某个元素，也能删除 dict （字典）

通过调用 `clear()` 方法可以清除字典中的所有元素

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333'}
print(dict1)

# 通过 key 值，删除对应的元素
del dict1['twowater']
print(dict1)

# 删除字典中的所有元素
dict1.clear()
print(dict1)

# 删除字典
del dict1
```

输出的结果：

```
{'liangdianshui': '111111', 'twowater': '222222', '两点水': '333333'}
{'liangdianshui': '111111', '两点水': '333333'}
{}
```

#### 6.4 dict（字典）使用时注意的事项

(1) dict （字典）是不允许一个键创建两次的，但是在创建 dict （字典）的时候如果出现了一个键值赋予了两次，会以最后一次赋予的值为准

例如：

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111' ,'twowater':'222222' ,'两点水':'333333','twowater':'444444'}
print(dict1)
print(dict1['twowater'])
```

输出的结果：

```
{'liangdianshui': '111111', 'twowater': '444444', '两点水': '333333'}
444444
```

(2) dict （字典）键必须不可变，可是键可以用数字，字符串或元组充当，但是就是不能使用列表

例如：

```python
#-*-coding:utf-8-*-
dict1={'liangdianshui':'111111', 123:'222222', (123,'tom'):'333333', 'twowater':'444444'}
print(dict1)
```

输出结果：

```
{'liangdianshui': '111111', 123: '222222', (123, 'tom'): '333333', 'twowater': '444444'}
```

#### 6.5 dict（字典）的特点和对比

1. 特点

dict 内部存放的顺序和 key 放入的顺序是没有任何关系

2. 对比

和 list 比较，dict 有以下几个特点：

- 查找和插入的速度极快，不会随着 key 的增加而变慢
- 需要占用大量的内存，内存浪费多

而 list 相反：

- 查找和插入的时间随着元素的增加而增加
- 占用空间小，浪费内存很少

#### 6.6 dict （字典） 的函数和方法

| 方法和函数     | 描述                                             |
| -------------- | ------------------------------------------------ |
| len(dict)      | 计算字典元素个数                                 |
| str(dict)      | 输出字典可打印的字符串表示                       |
| type(variable) | 返回输入的变量类型，如果变量是字典就返回字典类型 |
| dict.clear()   | 删除字典内所有元素                               |
| dict.copy()    | 返回一个字典的浅复制                             |
| dict.values()  | 以列表返回字典中的所有值                         |
| popitem()      | 随机返回并删除字典中的一对键和值                 |
| dict.items()   | 以列表返回可遍历的(键, 值) 元组数组              |

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
