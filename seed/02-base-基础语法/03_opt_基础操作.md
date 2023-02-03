<!--ts-->
<!--te-->

# 索引、截取、可迭代、遍历、拼接、重复

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

那些数据类型可迭代（可遍历）？

1. 字符串
2. 列表
