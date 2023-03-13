<!--ts-->

- [入门](#入门)
  - [索引](#索引)
  - [截取（切片）](#截取切片)
  - [拼接、重复](#拼接重复)
  - [可迭代、遍历](#可迭代遍历)
  - [什么是 print()函数](#什么是-print函数)
  - [什么是 range()函数](#什么是-range函数)
- [条件](#条件)
  - [if-else 基本形式](#if-else-基本形式)
  - [if-elif-else 多个判断条件](#if-elif-else-多个判断条件)
  - [if-elif-else 多个判断条件的组合](#if-elif-else-多个判断条件的组合)
  - [match-case](#match-case)
- [循环](#循环)
  - [while](#while)
  - [while xxx else](#while-xxx-else)
  - [while 同一行的简单语句](#while-同一行的简单语句)
  - [for](#for)
  - [for xx else yy](#for-xx-else-yy)
  - [break 中断、continue 继续](#break-中断continue-继续)
  - [pass](#pass)
  - [进阶](#进阶)
    - [1. for 和 while 的区别](#1-for-和-while-的区别)
    - [2. for 或 while xx else 的对比](#2-for-或-while-xx-else-的对比)
    - [3. 都可以嵌套](#3-都可以嵌套)
- [例子](#例子)

<!-- Added by: edy, at: 2023年 3月13日 星期一 16时11分59秒 CST -->

<!--te-->

# 入门

## 索引

索引值以 `0` 为开始值，`-1` 为从末尾的开始位置。

```python
# 012345
s = "Runoob"
# -6-5-4-3-2-1
```

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-4-string.py)
[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-5-list.py)

## 截取（切片）

那些数据类型可截取（切片）？

1. 字符串，截取返回字符串
2. 列表，截取返回列表

当截取时，索引范围规则：**左闭右开**

- 截取语法：`变量[头下标:尾下标]`，注意 **默认步长为 1**
- 另外，可以接收第三个参数：`变量[头下标:尾下标:步长(可选)]`，如果第三个参数为`负数`表示**逆向读取**

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-4-string.py)
[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-5-list.py)

## 拼接、重复

那些数据类型可拼接和重复？

1. 字符串
2. 列表

加号 `+` 是列表连接运算符，星号 `*` 是重复操作

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-4-string.py)
[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/term/02-5-list.py)

## 可迭代、遍历

那些数据类型可迭代（可遍历）？

1. 字符串
2. 列表

## 什么是 print()函数

[参考](../../site-packages/standard_lib/print/)

## 什么是 range()函数

[参考](../../site-packages/standard_lib/range/)

# 条件

[参考](https://github.com/walter201230/Python/blob/master/Article/PythonBasis/python5/If.md)

## if-else 基本形式

```python
if 判断条件：
    执行语句……
else：
    执行语句……
```

## if-elif-else 多个判断条件

1. 每个条件后面要使用`冒号 :`，表示接下来是满足条件后要执行的语句块
2. 使用缩进来划分语句块

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3

# 如果 "condition_1" 为 True 将执行 "statement_block_1" 块语句
# 如果 "condition_1" 为False，将判断 "condition_2"
# 如果"condition_2" 为 True 将执行 "statement_block_2" 块语句
# 如果 "condition_2" 为False，将执行"statement_block_3"块语句

# 可以嵌套

if 表达式1:
    语句
    if 表达式2:
        语句
    elif 表达式3:
        语句
    else:
        语句
elif 表达式4:
    语句
else:
    语句
```

## if-elif-else 多个判断条件的组合

> 注意：if 有多个条件时可使用括号来区分判断的先后顺序，括号中的判断优先执行

```python
# 这时候我们可以结合 or 和 and 来使用。
# or （或）表示两个条件有一个成立时判断条件成功
# and （与）表示只有两个条件同时成立的情况下，判断条件才成功。

# -*-coding:utf-8-*-

java = 86
python = 68

if java > 80 and  python > 80:
    print('优秀')
else :
    print('不优秀')

if ( java >= 80  and java < 90 )  or ( python >= 80 and python < 90):
    print('良好')

# 输出结果：
# 不优秀
# 良好
```

## match-case

> 类似 go 中的 `switch...case`

注意，**Python >=3.10** 增加了 `match...case` 的条件判断，不需要再使用一连串的 if-else 来判断了。

1. match 后的对象会依次与 case 后的内容进行匹配，如果匹配成功，则执行匹配到的表达式，否则直接跳过
2. case 后的 `_` 可以匹配一切。

> case `_` 类似于 C、Go 和 Java 中的 `default`:，当其他 case 都无法匹配时，匹配这条，保证永远会匹配成功。

语法格式如下：

```python
match subject:
    case <pattern_1>:
        <action_1>
    case <pattern_2>:
        <action_2>
    case <pattern_3>:
        <action_3>
    case _:
        <action_wildcard>

# 一个 case 也可以设置多个匹配条件，条件使用 ｜ 隔开，例如：
...
    case 401|403|404:
        return "Not allowed"

# 例子

mystatus=400
print(http_error(400))

def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"
```

# 循环

计算机最擅长就是做重复的事情。

## while

如果 while 后面的条件语句为 true 时，则执行 statements 语句块。

```python
while 判断条件(condition)：
    执行语句(statements)
```

- 无限循环

```python
var = 1
while var == 1 :  # 表达式永远为 true {条件永远成立}
   num = int(input("输入一个数字  :"))
   print ("你输入的数字是: ", num)

print ("Good bye!")
```

## while xxx else

如果 while 后面的条件语句为 false 时，则执行 else 的语句块。

```python
while <expr>:
    <statement(s)>
else:
    <additional_statement(s)>

# expr 条件语句为 true 则执行 statement(s) 语句块，如果为 false，则执行 additional_statement(s)。

count = 0
while count < 5:
   print (count, " 小于 5")
   count = count + 1
else:
   print (count, " 大于或等于 5")
```

## while 同一行的简单语句

如果你的 while **循环体中只有一条语句**，你可以将该语句与 while 写在同一行中

```python
#!/usr/bin/python

flag = 1

while (flag): print ('欢迎访问菜鸟教程!')

print ("Good bye!")
```

## for

Python for 循环可以**遍历任何可迭代对象**，如：一个列表或者一个字符串。

```python
for <variable> in <sequence>:
    <statements>
else:
    <statements>

# 例子
sites = ["Baidu", "Google","Runoob","Taobao"]
for site in sites:
    print(site)

# 整数范围值可以配合 range() 函数使用, 1 到 5 的所有数字：
for number in range(1, 6):
    print(number)
```

## for xx else yy

`for...else` 语句用于在循环结束（没有中断）后执行一段代码。

1. 当**循环执行完毕（即遍历完 iterable 中的所有元素）**后，会执行 else 子句中的代码。有点类似回调函数。
2. 如果在循环过程中遇到了 break 语句，则会中断循环，此时不会执行 else 子句。

```python
for item in iterable:
    # 循环主体
else:
    # 循环结束后执行的代码

# 例子
for x in range(6):
  print(x)
else:
  print("Finally finished!")

# 若触发使用了 break 语句，break 语句用于跳出当前循环体（造成循环中断），不会执行 else 子句
sites = ["Baidu", "Google","Runoob","Taobao"]
for site in sites:
    if site == "Runoob":
        print("菜鸟教程!")
        break
    print("循环数据 " + site)
else:
    print("没有循环数据!")
print("完成循环!")
```

## break 中断、continue 继续

- break 语句可以跳出 for 和 while 的**当前循环体**
- continue 语句跳过当前循环块中的剩余语句，然后**继续**进行下一轮循环。

## pass

pass 是空语句，是为了保持程序结构的完整性。pass 不做任何事情，一般用做`占位语句`，如下实例

## 进阶

### 1. for 和 while 的区别

那什么时候才使用 for 循环和 while 循环呢？

- for 循环主要用在迭代可迭代对象的情况。
- while 循环主要用在需要满足一定条件为真，反复执行的情况。（死循环+break 退出等情况。）
- 部分情况下，for 循环和 while 循环可以互换使用。

### 2. for 或 while xx else 的对比

```python
for xxx else
while xxx else
```

当然有 `for … else` ，也会有 `while … else` 。

**他们的意思都是一样的**，举例说明如下：

- 在循环正常执行完（不是通过 break 等跳出而中断的）情况下，都会执行 else 代码块

> for, while 正常结束，都是自身的循环条件为 False 时结束

### 3. 都可以嵌套

循环语句和条件语句一样，都是可以嵌套的。

```python
# for 循环嵌套语法
for iterating_var in sequence:
   for iterating_var in sequence:
      statements(s)
   statements(s)

# while 循环嵌套语法
while expression:
   while expression:
      statement(s)
   statement(s)

# 除此之外，你也可以在循环体内嵌入其他的循环体，如在 while 循环中可以嵌入 for 循环， 反之，你可以在 for 循环中嵌入 while 循环
```

# 例子

[code](https://github.com/andytyc/pythoncode/blob/main/seed/base/opt/03-1-if-else-for-while.py)
