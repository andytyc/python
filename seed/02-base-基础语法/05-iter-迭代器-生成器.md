<!--ts-->

- [迭代器（对象）](#迭代器对象)
  - [介绍和理解](#介绍和理解)
  - [自定义创建一个迭代器](#自定义创建一个迭代器)
    - [类](#类)
      - [1. 实现迭代器](#1-实现迭代器)
      - [2. StopIteration 结束迭代](#2-stopiteration-结束迭代)
- [生成器](#生成器)
  - [介绍和理解](#介绍和理解-1)
  - [例子](#例子)

<!-- Added by: edy, at: 2023年 3月15日 星期三 15时57分53秒 CST -->

<!--te-->

# 迭代器（对象）

## 介绍和理解

迭代是 Python 最强大的功能之一，是访问集合元素的一种方式。

- 迭代器是一个可以记住遍历的位置的对象（是一个对象）。

- 迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。

迭代器有两个基本的方法：

- iter() 方法，返回一个迭代器对象，它可以记录当前遍历的位置（索引）。
- next() 方法，访问下一个元素（访问当前位置元素，并将位置往前移动），并通过 `StopIteration` 异常标识迭代的完成。

> 能够创建迭代器的对象，都成为：可迭代的对象

字符串，列表或元组对象（可迭代对象）都可用于创建迭代器：

```python
>>> list=[1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> print (next(it))   # 输出迭代器的下一个元素
1
>>> print (next(it))
2
>>>
```

迭代器对象可以使用常规 for 语句进行遍历：

```python
#!/usr/bin/python3

list=[1,2,3,4]
it = iter(list)    # 创建迭代器对象
for x in it:
    print (x, end=" ")

# 1 2 3 4
```

也可以使用 next()方法实现上边 for 遍历一样的效果：

```python
#!/usr/bin/python3

import sys         # 引入 sys 模块

list=[1,2,3,4]
it = iter(list)    # 创建迭代器对象

while True:
    try:
        print (next(it))
    except StopIteration:
        sys.exit()

# 执行以上程序，输出结果如下：
# 1
# 2
# 3
# 4
```

## 自定义创建一个迭代器

上边，一些现成的迭代器，比如：字符串、列表、元组，这里学习下如何自己创建（实现）一个迭代器。

> 简单理解：什么是迭代器对象？就是实现了迭代器方法的对象。

### 类

#### 1. 实现迭代器

把一个类作为一个迭代器使用（用类实现迭代器），需要在类中实现两个方法： `__iter__()` 与 `__next__()`

如果已经了解的面向对象编程，就知道：

- `__init__()`构造方法，类都会有这样一个构造函数, 它会在对象初始化的时候执行。
- `__iter__()` 方法返回一个特殊的迭代器对象，这个迭代器对象实现了 `__next__()` 方法并通过 `StopIteration` 异常标识迭代的完成。

> 注意：`__next__()` 方法（Python 2 里是 next()）会返回下一个迭代器对象。

创建一个返回数字的迭代器，初始值为 1，逐步递增 1：

```python
# 创建一个迭代器 MyNumbers
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self     # 返回一个迭代器对象 self ，为什么self是迭代器对象？因为 self 自己实现了 __next__ 方法

  def __next__(self):
    x = self.a
    self.a += 1
    return x

myclass = MyNumbers()    # myclass 迭代器对象（实现了迭代器方法）
myiter = iter(myclass)    # iter() 返回的是 self 也就是 myclass 自己，也就是迭代器对象

print(next(myiter))   # 执行迭代器对象 myiter/myclass 的__next__方法
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))

# 执行输出结果为：
# 1
# 2
# 3
# 4
# 5
```

#### 2. StopIteration 结束迭代

但是，这个例子有一个问题？

就是迭代次数没有上限，如果放进循环里迭代，会一直持续下去，所以加一个 `StopIteration` 异常标识：

> StopIteration 异常用于标识迭代的完成，防止出现无限循环的情况，在 `__next__()` 方法中我们可以设置在完成指定循环次数后触发 StopIteration 异常来结束迭代

在 20 次迭代后停止执行：

```python
# 创建一个迭代器 MyNumbers
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self     # 返回一个迭代器对象 self ，为什么self是迭代器对象？因为 self 自己实现了 __next__ 方法

  def __next__(self):
    if self.a <= 20:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration   # 抛出迭代结束异常：StopIteration

myclass = MyNumbers()    # myclass 迭代器对象（实现了迭代器方法）
myiter = iter(myclass)    # iter() 返回的是 self 也就是 myclass 自己，也就是迭代器对象

for x in myiter:
  print(x)

# 执行输出结果为：
# 1
# 2
# 3
# ....
# 19
# 20
```

# 生成器

在 Python 中，使用了 yield 的函数被称为生成器（generator）。

## 介绍和理解

什么是生成器？它如何使用？

- 使用了 yield 的函数被称为生成器（生成器函数）。
- 调用一个生成器函数，**返回的是一个迭代器对象，并且它只能用于迭代操作**（只能执行 next()方法）。
- 在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值，并在下一次执行 next() 方法时从当前位置继续运行。

使用场景：

- 在进行复杂算法封装时，能够合理使用生成器（yield）会让算法过程变得更清晰、更优雅、更简洁。

## 例子

以下实例使用 yield 实现斐波那契数列：

```python
#!/usr/bin/python3

import sys

def fibonacci(n):  # 生成器函数 - 斐波那契
    a, b, counter = 0, 1, 0
    while True:
        if counter > n:
            return
        yield a
        a, b = b, a + b
        counter += 1

f = fibonacci(10)  # f 是一个迭代器，由生成器返回生成

while True:
    try:
        print(next(f), end=" ")  # 生成器返回的迭代器对象 f ，这个 f 只能用于 next(f) 方法
    except StopIteration:
        print("\niter.next() is end")
        sys.exit()

# 输出
# 0 1 1 2 3 5 8 13 21 34 55
# iter.next() is end
```
