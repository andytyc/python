<!--ts-->

- [模块](#模块)
  - [import 入门使用](#import-入门使用)
    - [import xxx](#import-xxx)
    - [from xxx import yyy](#from-xxx-import-yyy)
      - [特殊（不推荐）](#特殊不推荐)
  - [内置属性、内置方法](#内置属性内置方法)
    - [--name--](#--name--)
    - [dir()](#dir)
- [包 package](#包-package)
  - [import 深入理解](#import-深入理解)
  - [--init--.py 特殊模块](#--init--py-特殊模块)
    - [--all-- 内置属性](#--all---内置属性)

<!-- Added by: edy, at: 2023年 2月 6日 星期一 18时03分30秒 CST -->

<!--te-->

# 模块

什么是模块？

> 一个源代码文件（`xxx.py`）就是一个模块，可通过文件路径进行导入

1. 模块是一个包含所有你定义的函数和变量的文件，其后缀名是 `xxx.py`
2. 模块可以被别的程序引入，以使用该模块中的函数等功能，以及`一些初始化操作、内置函数或内置属性`

什么是 import 语句？

1. 一个模块只会被导入一次，不管你执行了多少次 import

> Python 的搜索路径：搜索路径是由一系列目录名组成的，Python 解释器就依次从这些目录中去寻找所引入的模块。

模块包有初始化操作吗？

有。模块除了方法定义，还可以包括可执行的代码。这些代码一般用来初始化这个模块。这些代码只有在第一次被导入时才会被执行

> 详细，看下边例子

## import 入门使用

### import xxx

```python
#!/usr/bin/python3
# Filename: support.py

def print_func( par ):
    print ("Hello : ", par)
    return
```

test.py 引入 support 模块：

```python
#!/usr/bin/python3
# Filename: test.py

# 导入模块
import support

# 现在可以调用模块里包含的函数了
support.print_func("Runoob")
```

### from xxx import yyy

可以从模块中导入一个指定的部分到当前命名空间中

格式：

```bash
from modname import name1[, name2[, ... nameN]]

modname
# 模块，也就是 modname.py

name1
# 变量、方法等
```

例子，这个声明不会把整个 fibo 模块导入到当前的命名空间中，它只会将 fibo 里的 fib 函数引入进来

```python
# 斐波那契(fibonacci)数列模块
# Filename: fibo.py

def fib(n):    # 定义到 n 的斐波那契数列
    a, b = 0, 1
    while b < n:
        print(b, end=' ')
        a, b = b, a+b
    print()

def fib2(n): # 返回到 n 的斐波那契数列
    result = []
    a, b = 0, 1
    while b < n:
        result.append(b)
        a, b = b, a+b
    return result
```

```python
# 导入模块 fibo 的 fib 函数
from fibo import fib, fib2

num = fib(500)
print(num)
```

#### 特殊（不推荐）

这种声明不该被过多地使用（不建议使用）

```python
# * 把一个模块的所有内容（声明：变量、方法）全都导入
from modname import *
```

## 内置属性、内置方法

### --name--

内置属性，运行或导入时判断。每个模块都有一个 `__name__` 属性，当其值是 `'__main__'` 时，表明该模块自身在运行，否则是被导入的

应用场景：

如果我们想在模块被引入时，模块中的某一程序执行块不执行，我们可以用`__name__`属性来使该程序块仅在该模块自身运行时执行。

```python
#!/usr/bin/python3
# Filename: using_name.py

if __name__ == '__main__':
   print('程序自身在运行')
else:
   print('我来自另一模块')
```

```bash
# 执行当前模块自身
$ python using_name.py
程序自身在运行

# 通过导入import模块来使用
$ python
>>> import using_name
我来自另一模块
```

### dir()

内置函数，可以找到模块内定义的所有名称（所有的声明）。

```bash
#########
# 以一个字符串列表的形式返回
#########

>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']
>>> dir(sys)
['__displayhook__', '__doc__', '__excepthook__', '__loader__', '__name__',
 '__package__', '__stderr__', '__stdin__', '__stdout__',
 '_clear_type_cache', '_current_frames', '_debugmallocstats', '_getframe',
 '_home', '_mercurial', '_xoptions', 'abiflags', 'api_version', 'argv',
 'base_exec_prefix', 'base_prefix', 'builtin_module_names', 'byteorder',
 'call_tracing', 'callstats', 'copyright', 'displayhook',
 'dont_write_bytecode', 'exc_info', 'excepthook', 'exec_prefix',
 'executable', 'exit', 'flags', 'float_info', 'float_repr_style',
 'getcheckinterval', 'getdefaultencoding', 'getdlopenflags',
 'getfilesystemencoding', 'getobjects', 'getprofile', 'getrecursionlimit',
 'getrefcount', 'getsizeof', 'getswitchinterval', 'gettotalrefcount',
 'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info',
 'intern', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path',
 'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'ps1',
 'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit',
 'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdout',
 'thread_info', 'version', 'version_info', 'warnoptions']

#########
# 如果没有给定参数，那么 dir() 函数会罗列出当前定义的所有名称
#########

>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir() # 得到一个当前模块中定义的属性列表
['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
>>> a = 5 # 建立一个新的变量 'a'
>>> dir()
['__builtins__', '__doc__', '__name__', 'a', 'sys']
>>>
>>> del a # 删除变量名a
>>>
>>> dir()
['__builtins__', '__doc__', '__name__', 'sys']
>>>
```

# 包 package

可以看着 包 是一个或多个模块的集合（目录）

什么目录可以作为一个包？

1. 目录只有包含一个叫做 `__init__.py` 的文件才会被认作是一个包

包是一种管理 Python 模块命名空间的形式，采用"点模块名称"。采用点模块名称这种形式，也不用担心不同库（包）之间的模块重名的情况

> 比如一个模块的名称是 A.B， 那么他表示一个包 A 中的子模块 B

通过例子来理解：

假设，你想设计一套统一处理声音文件和数据的模块（或者称之为一个"包"）。

现存很多种不同的音频文件格式（基本上都是通过后缀名区分的，例如： .wav，:file:.aiff，:file:.au，），所以你需要有一组不断增加的模块，用来在不同的格式之间转换。

并且针对这些音频数据，还有很多不同的操作（比如混音，添加回声，增加均衡器功能，创建人造立体声效果），所以你还需要一组怎么也写不完的模块来处理这些操作。

这里给出了一种可能（模拟）的包结构（在分层的文件系统中）:

```bash
sound/                          顶层包
      __init__.py               初始化 sound 包 （包目录有: __init__.py）
      formats/                  文件格式转换子包
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  声音效果子包
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  filters 子包
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

> 可以看出，包：sound 子包：formats,effects,filters

## import 深入理解

```python
############# 1: 导入模块（全路径） #############

# 用户可以每次只导入一个包（sound.effects）里面的特定模块（echo.py），比如:
import sound.effects.echo

# 这将会导入子模块:sound.effects.echo，这样必须使用全名去访问:
sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)

############# 2: 导入模块（命名） #############

# 还有一种导入子模块（echo.py）的方法是:
from sound.effects import echo

# 这同样会导入子模块: echo，并且他不需要那些冗长的前缀，所以他可以这样使用:
echo.echofilter(input, output, delay=0.7, atten=4)

############# 3: 导入模块内函数/方法 #############

# 还有一种变化就是直接导入一个函数或者变量:
from sound.effects.echo import echofilter

# 同样的，这种方法会导入子模块: echo，并且可以直接使用他的 echofilter() 函数:
echofilter(input, output, delay=0.7, atten=4)
```

## --init--.py 特殊模块

也就是每个包的 `__init__.py` 文件

### --all-- 内置属性

```python
############# 4: 导入模块内所有声明（*，不推荐！！） #############

from sound.effects import *
```

这个方法在 Windows 平台上工作的就不是非常好，因为 Windows 是一个不区分大小写的系统。在 Windows 平台上，我们无法确定一个叫做 ECHO.py 的文件导入为模块是 echo 还是 Echo，或者是 ECHO。

为了解决这个问题，我们只需要提供一个**精确包的索引**

导入语句遵循如下规则：

1. 如果包定义文件 `__init__.py` 存在一个叫做 `__all__` 的列表变量，那么在使用 `from package import *` 的时候就把这个列表中的所有名字作为包内容导入。

比如：

```python
# sounds/effects/__init__.py
# 参考:https://www.runoob.com/python3/python3-module.html

__all__ = ["echo", "surround", "reverse"]
```

这表示，当你使用 `from sound.effects import *` 这种用法时，你只会导入包里面这三个子模块。
