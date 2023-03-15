<!--ts-->

- [面向对象的概念](#面向对象的概念)
  - [1. 面向对象的两个基本概念](#1-面向对象的两个基本概念)
  - [2. 面向对象的三大特性](#2-面向对象的三大特性)
  - [3. 概念术语](#3-概念术语)
- [类和对象](#类和对象)
  - [类是什么](#类是什么)
  - [怎么定义类](#怎么定义类)
  - [怎么调用类属性和类方法](#怎么调用类属性和类方法)
  - [类对象是什么](#类对象是什么)
  - [特殊标识符](#特殊标识符)
    - [self](#self)
  - [类属性](#类属性)
    - [1. 私有属性](#1-私有属性)
  - [类方法](#类方法)
    - [1. 常见例子（入门）](#1-常见例子入门)
    - [2. 私有方法](#2-私有方法)
    - [3. 类的专有方法](#3-类的专有方法)
      - [3.1 构造方法 init](#31-构造方法-init)
      - [3.2 析构函数 del](#32-析构函数-del)
      - [3.3 其他方法](#33-其他方法)
- [继承](#继承)
  - [单继承、多继承、重写方法](#单继承多继承重写方法)
  - [重写时选择调用父类方法](#重写时选择调用父类方法)
    - [1. 子类内部使用](#1-子类内部使用)
    - [2. 子类的对象使用](#2-子类的对象使用)

<!-- Added by: edy, at: 2023年 3月15日 星期三 19时34分16秒 CST -->

<!--te-->

# 面向对象的概念

## 1. 面向对象的两个基本概念

编程语言中，一般有两种编程思维，`面向过程`和`面向对象`。

- 面向过程，看重的是解决问题的过程。这好比我们解决日常生活问题差不多，分析解决问题的步骤，然后一步一步的解决。

- 面向对象是一种抽象，抽象是指用分类的眼光去看世界的一种方法。

Python 就是一门面向对象的语言,

> 如果你学过 Java ，就知道 Java 的编程思想就是：万事万物皆对象。Python 也不例外，在解决实际问题的过程中，可以把构成问题事务分解成各个对象。

面向对象都有两个基本的概念，分别是类和对象。

- **类**

用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。

- **对象**

通过类定义的数据结构实例

## 2. 面向对象的三大特性

面向对象的编程语言，也有三大特性，继承，多态和封装性。

- **继承**

即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。

例如：一个 Dog 类型的对象派生自 Animal 类，这是模拟"是一个（is-a）"关系（例图，Dog 是一个 Animal ）。

- **多态**

它是指对不同类型的变量进行相同的操作，它会根据对象（或类）类型的不同而表现出不同的行为。

- **封装性**

封装就是将抽象得到的数据和行为（或功能）相结合，形成一个有机的整体（即类）；

封装的目的：是增强安全性和简化编程，使用者不必了解具体的实现细节，而只是要通过外部接口，一特定的访问权限来使用类的成员。

## 3. 概念术语

- **类(Class):** 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。
- **方法：**类中定义的函数。
- **类变量：**类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。
- **数据成员：**类变量或者实例变量，用于处理类及其实例对象的相关的数据。
- **方法重写：**如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
- **局部变量：**定义在方法中的变量，只作用于当前实例的类。
- **实例变量：**在类的声明中，属性是用变量来表示的，这种变量就称为实例变量，实例变量就是一个用 self 修饰的变量。
- **继承：**即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个 Dog 类型的对象派生自 Animal 类，这是模拟"是一个（is-a）"关系（例图，Dog 是一个 Animal）。
- **实例化：**创建一个类的实例，类的具体对象。
- **对象：**通过类定义的数据结构实例。对象包括：两种数据成员（类变量和实例变量）和方法。

# 类和对象

## 类是什么

简单理解就是：类是一个变量和函数的集合。把变量和函数包装在一起。

> 把同性质的包装在一个类里，这样就方便我们重复使用。

## 怎么定义类

类定义语法格式如下：

```python
class ClassName():
    <statement-1>
    .
    .
    .
    <statement-N>
```

可以看到，我们是用 `class` 语句来自定义一个类的，其实这就好比我们是用 `def` 语句来定义一个函数一样。

说类是变量和方法的集合包，那么我们来创建一个类。

## 怎么调用类属性和类方法

我们定义了类之后，那么我们怎么调用类里面的属性和方法呢？

- 类里边的变量叫属性，怎样调用？格式：`类.属性`
- 类里边的函数叫方法，怎样调用？格式：`类.函数()`

## 类对象是什么

类对象支持两种操作：

- 属性引用。属性引用的标准语法：`obj.name`
- 实例化。语法：`对象 = 类()`

```python
class ClassA:
    var1 = 100
    var2 = 0.01
    var3 = "两点水"

    def fun1(self):
        print("我是 fun1")

    def fun2(self):
        print("我是 fun2")

    def fun3(self):
        print("我是 fun3")


# 实例化（类对象）, 创建了一个新的类实例并将该对象赋给局部变量 boy
boy = ClassA()
# 调用属性
print(boy.var1)
print(boy.var2)
print(boy.var3)
# 调用方法
boy.fun1()
boy.fun2()
boy.fun3()

# 100
# 0.01
# 两点水
# 我是 fun1
# 我是 fun2
# 我是 fun3
```

## 特殊标识符

这些标识符，结合着：类方法例子看，能够更好的理解

### self

它是什么？

- self 就是代指这个类的实例对象（为什么代指？因为声明类时，实例化还么有进行，只是控制内部属性和方法调用的对象）

- 类的方法与普通的函数只有一个特别的区别：它们必须有一个额外的**第一个参数名称**, 按照惯例它的名称是 self，只是一个大家都认同的一个**习惯名称**，self 不是 python 关键字，这个习惯名称当然也可以换个名称，比如：runoob

> self 名称虽然是一个约定可以修改任意名称，但最好还是按照约定来，这样大家互相阅读代码时更加友好

```python
class Test:
    def prt(self):
        print(self)
        print(self.__class__)

t = Test()
t.prt()

#从执行结果可以很明显的看出，self 代表的是类的实例，代表当前对象的地址，而 self.class 则指向类

#self 不是 python 关键字，我们把他换成比如： runoob 也是可以正常执行的

class Test2:
    def prt(runoob):
        print(runoob)
        print(runoob.__class__)

t2 = Test2()
t2.prt()

#<__main__.Test object at 0x10cd190b8>
#<class '__main__.Test'>
#<__main__.Test2 object at 0x10cd19128>
#<class '__main__.Test2'>
```

## 类属性

### 1. 私有属性

`__private_attrs`：两个下划线开头，声明该属性为私有，不能在类的外部被使用或直接访问。在类内部的方法中使用时 `self.__private_attrs`。

```python
class JustCounter:
    __secretCount = 0  # 私有变量
    publicCount = 0  # 公开变量

    def count(self):
        self.__secretCount += 1  # 类内部可以调用私有属性
        self.publicCount += 1
        print("count:", self.__secretCount)


counter = JustCounter()
counter.count()
counter.count()
print(counter.publicCount)  # 正常
print(counter.__secretCount)  # 报错(实例不能访问私有变量)

# count: 1
# count: 2
# 2
# Traceback (most recent call last):
#   File "/Users/edy/go/src-rep/pythoncode/seed/base/obj/06-1-obj.py", line 118, in <module>
#   print(counter.__secretCount)  # 报错(实例不能访问私有变量)
# AttributeError: 'JustCounter' object has no attribute '__secretCount'
```

## 类方法

在类的内部，使用 def 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 **self**，且为第一个参数，**self** 代表的是类的实例。

### 1. 常见例子（入门）

```python
# 类定义
class People:
    # 定义基本属性
    name = ""
    age = 0
    # 定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0

    # 定义构造方法
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w

    def speak(self):
        print("%s 说: 我 %d 岁, 重 %d" % (self.name, self.age, self.__weight))


# 实例化类
p = People("runoob", 10, 30)
# 调用实例方法
p.speak()

# runoob 说: 我 10 岁, 重 30
```

### 2. 私有方法

`__private_method`：两个下划线开头，声明该方法为私有方法，只能在类的内部调用 ，不能在类的外部调用。`self.__private_methods`。

```python
class Site:
    def __init__(self, name, url):
        self.name = name  # public
        self.__url = url  # private

    def who(self):
        print("name  : ", self.name)
        print("url : ", self.__url)

    def __foo(self, w):  # 私有方法
        print("这是私有方法", w)

    def foo(self):  # 公共方法
        print("这是公共方法")
        self.__foo("公共foo调用")  # 类内部可以调用私有方法


x = Site("菜鸟教程", "www.runoob.com")
x.who()  # 正常输出
x.foo()  # 正常输出
x.__foo()  # 报错(类外部不能调用私有方法), AttributeError: 'Site' object has no attribute '__foo'

# name  :  菜鸟教程
# url :  www.runoob.com
# 这是公共方法
# 这是私有方法 公共foo调用
# Traceback (most recent call last):
# 	File "/Users/edy/go/src-rep/pythoncode/seed/base/obj/06-1-obj.py", line 101, in <module>
# 	x.__foo()  # 报错
# AttributeError: 'Site' object has no attribute '__foo'
```

### 3. 类的专有方法

#### 3.1 构造方法 init

类有一个名为 `__init__()` 的特殊方法（**构造方法**），该方法在类实例化时会自动调用（在生成对象时调用）。

像下面这样：

```python
class MyClass:

  def __init__(self):
      self.data = []

# 类的实例化操作会自动调用 __init__() 方法
x = MyClass()
```

可以有参数，参数通过 `__init__()` 传递到类的实例化操作上。例如:

```python
#!/usr/bin/python3

class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart

x = Complex(3.0, -4.5)
print(x.r, x.i)   # 输出结果：3.0 -4.5
```

#### 3.2 析构函数 del

析构函数，释放对象时使用

```python
# 类定义
class People2:
    # 定义基本属性
    name = ""
    age = 0
    # 定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0

    # 定义构造方法
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w

    def speak(self):
        print("%s 说: 我 %d 岁, 重 %d" % (self.name, self.age, self.__weight))

    def __del__(self):
        # 实例释放资源时自动调用
        print("i'm game over", self.name)


# 实例化类
p2 = People2("runoob2", 10, 30)
# 调用实例方法
p2.speak()

# runoob2 说: 我 10 岁, 重 30
# i'm game over runoob2
```

#### 3.3 其他方法

有关于打印输出的，有关于计算的，其实可以看出很多都是以算法目标创建的一些方法（可以方便""偷懒""）：

```bash
__init__ : 构造函数，在生成对象时调用
__del__ : 析构函数，释放对象时使用
__repr__ : 打印，转换
__setitem__ : 按照索引赋值
__getitem__: 按照索引获取值
__len__: 获得长度
__cmp__: 比较运算
__call__: 函数调用
__add__: 加运算
__sub__: 减运算
__mul__: 乘运算
__truediv__: 除运算
__mod__: 求余运算
__pow__: 乘方
```

比如：

```python
class Vector:
    def __init__(self, a, b):
        self.a = a
        self.b = b

    def __str__(self):
        return "Vector (%d, %d)" % (self.a, self.b)  # print()打印输出时，会执行这个__str__方法

    def __add__(self, other):
        return Vector(self.a + other.a, self.b + other.b)  # 返回一个新的Vector实例对象


v1 = Vector(2, 10)
v2 = Vector(5, -2)
print(v1 + v2) # + 加运算触发__add__, print打印触发__str__

# runoob2 说: 我 10 岁, 重 30
# Vector (7, 8)
```

# 继承

Python 同样支持类的继承，如果不支持继承，类就没有什么意义。

派生类的定义如下所示:

```python
# 子类（派生类 DerivedClassName）会继承父类（基类 BaseClassName）的属性和方法。
class DerivedClassName(BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>

# BaseClassName 基类若定义在另一个模块(modname)中时，导入即可:
class DerivedClassName(modname.BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>
```

## 单继承、多继承、重写方法

- 单继承(单个父类)，多重继承(多个父类)。
- 如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法

在下边例子中理解：

```python
# 类定义
class People:
    # 定义基本属性
    name = ""
    age = 0
    # 定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0

    # 定义构造方法
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w

    def speak(self):
        print("%s 说: 我 %d 岁 重 %d" % (self.name, self.age, self.__weight))


# 单继承(单个父类)
class Student(People):
    grade = ""

    # 重写构造方法
    def __init__(self, n, a, w, g):
        # 调用父类的构函 (这样就实现了：在People初始化基础上，再定制化Student的一些初始化)
        People.__init__(self, n, a, w)  # 还有种方式，使用 super 方法
        self.grade = g

    # 重写/覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级" % (self.name, self.age, self.grade))


s = People("peo", 10, 60)
s.speak()

s = Student("stu", 10, 60, 3)
s.speak()


# 单继承(单个父类)
class Student66(People):
    grade = ""

    # 重写构造方法
    def __init__(self, n, a, w, g):
        # 调用父类的构函 (这样就实现了：在People初始化基础上，再定制化Student的一些初始化)
        People.__init__(self, n, a, w)
        self.grade = g

    # 重写/覆写父类的方法
    def speak(self):
        # 调用父类的speak
        People.speak(self)
        print("\n%s 我还有话说:\n" % self.name)
        print("%s 说: 我 %d 岁了，我在读 %d 年级" % (self.name, self.age, self.grade))


s = Student66("stu66", 10, 60, 3)
s.speak()


# 另一个类，多重继承之前的准备
class Speaker:
    topic = ""
    name = ""

    def __init__(self, n, t):
        self.name = n
        self.topic = t

    def speak(self):
        print("我叫 %s，我是一个演说家，我演讲的主题是 %s" % (self.name, self.topic))


# 多重继承(多个父类)
class Sample(Speaker, Student):
    a = ""

    def __init__(self, n, a, w, g, t):
        Student.__init__(self, n, a, w, g)
        Speaker.__init__(self, n, t)


many = Sample("man", 25, 80, 4, "Python")
many.speak()  # 方法名同，默认调用的是在括号中参数位置排前父类的方法

# peo 说: 我 10 岁 重 60
# stu 说: 我 10 岁了，我在读 3 年级
# stu66 说: 我 10 岁 重 60
#
# stu66 我还有话说:
#
# stu66 说: 我 10 岁了，我在读 3 年级
# 我叫 man，我是一个演说家，我演讲的主题是 Python
```

## 重写时选择调用父类方法

在继承的类中，如果不管有没有重写了父类方法，当从子类的角度进行调用父类的方法时？该怎么办呢？

### 1. 子类内部使用

在子类内部，两种方式：

1. 父类名称.类方法(self,参数 1，参数 2，...)

2. super(子类，self).类方法(参数 1，参数 2，....)

在上边继承的例子里用的就是第一种，下边的例子来看看 super 第二种的使用：

```python
# 类定义
class People77:
    # 定义基本属性
    name = ""
    age = 0
    # 定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0

    # 定义构造方法
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w

    def speak(self):
        print("%s 说: 我 %d 岁 重 %d" % (self.name, self.age, self.__weight))


# 单继承(单个父类)
class Student77(People77):
    grade = ""

    # 重写构造方法
    def __init__(self, n, a, w, g):
        # 调用父类的构函 (这样就实现了：在People初始化基础上，再定制化Student的一些初始化)
        # People.__init__(self, n, a, w)  # 还有种方式，使用 super 方法
        super(Student77, self).__init__(n, a, w)  # 使用super方法
        self.grade = g

    # 重写/覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级" % (self.name, self.age, self.grade))


s = People77("peo77", 10, 60)
s.speak()

s = Student77("stu77", 10, 60, 3)
s.speak()

# peo77 说: 我 10 岁 重 60
# stu77 说: 我 10 岁了，我在读 3 年级
```

### 2. 子类的对象使用

在类外部，也就是类的实例化对象如何调用它所属类父类的方法呢？

使用`super`就可以，例子如下：

```python
# 类定义
class People77:
    # 定义基本属性
    name = ""
    age = 0
    # 定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0

    # 定义构造方法
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w

    def speak(self):
        print("%s 说: 我 %d 岁 重 %d" % (self.name, self.age, self.__weight))


# 单继承(单个父类)
class Student77(People77):
    grade = ""

    # 重写构造方法
    def __init__(self, n, a, w, g):
        # 调用父类的构函 (这样就实现了：在People初始化基础上，再定制化Student的一些初始化)
        # People.__init__(self, n, a, w)  # 还有种方式，使用 super 方法
        super(Student77, self).__init__(n, a, w)  # 使用super方法
        self.grade = g

    # 重写/覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级" % (self.name, self.age, self.grade))


s = People77("peo77", 10, 60)
s.speak()

s = Student77("stu77", 10, 60, 3)
s.speak()
super(Student77, s).speak()  # s作为子类(Student77)的对象，调用父类(People77)的方法

# peo77 说: 我 10 岁 重 60
# stu77 说: 我 10 岁了，我在读 3 年级
# stu77 说: 我 10 岁 重 60
```
