---
title: python入门-2
date: 2023-01-29 17:07:31
tags: python
---
# Directory
- 解析
  - 列表解析
  - 集合解析
  - 字典解析
- 条件判断
- 循环
  - for 循环
  - while 循环
- 元组
- 字典
- 函数
- 调用
<!-- more -->
# 解析
## 概念
- 列表解析、集合解析、元组解析、字典解析。
- 根据某些元素来创建(推导)出一个新的列表、集合、元组、字典等。所以有的地方也称为推导，比如列表推导、集合推导等。
- 中括号，表示列表解析
- 大括号，表示集合解析
- 大括号且元素是key:value模式，表示字典解析
- 注意：如果使用的是括号，表示的是生成器表达式，而不是解析
## 列表解析
```py
my_list=[i*2 for i in range(10) if i % 2 == 0]
# [0, 4, 8, 12, 16]
```
## 集合解析
```py
{ i*2 for i in "abcd"}
# {'aa', 'cc', 'dd', 'bb'}
```
## 字典解析
```py
{ k:v for k,v in zip(("one","two","three"),(1,2,3)) }
# {'one':1, 'two':2, 'three':3}
{ k: k*2 for k in "abcd" }
# {'a':'aa', 'b':'bb', 'c':'cc', 'd':'dd'}
```
# 条件判断
## if else
- 缩进：
Python 依赖缩进，使用空格来定义代码中的范围。其他编程语言通常使用花括号来实现此目的。
- ``if:``
  - 简写``if``:如果只有一条语句要执行，则可以将其与 if 语句放在同一行。
  - 简写``if...else``，如：``if a > b else print("B")``
- ``elif``：else if，表示：如果之前的条件不正确，那么试试这个条件
- ``else``，捕获违背之前条件捕获的任何内容
- 嵌套``if``
- ``pass``：continue
## 组合条件语句
- ``and``：且 
```py
# a是否大于b 且c是否大于a：
a = 200
b = 66
c = 500
if a > b and c > a:
  print("Both conditions are True")
```
- ``or``：或
# 循环
## for循环
### basis
- for 循环用于迭代序列（即列表，元组，字典，集合或字符串）。
- 这与其他编程语言中的 for 关键字不太相似，而是更像其他面向对象编程语言中的迭代器方法。
- 循环遍历字符串
```py
for x in "banana":
  print(x)
```
- ``break``
- ``continue``
- ``pass``
- 嵌套循环
### ``range``
range() 函数返回一个数字序列，默认情况下从0开始，并默认递增 1，并以指定的数字结束。
- 注：``range(10)``不是0到10的值，而是0到9。
- ``range(3, 10)``表示``[3,9]``
- 指定增量值，(默认为1)，``range(0,20,2)``
```py
s=input()
for i in range(100):
    print(s,end="")
# print(s*100)
```
### ``for``循环中的``else``
- for 循环中的 else 关键字指定循环结束时要执行的代码块
```py
# 打印 0 到 9 的所有数字，并在循环结束时打印一条消息：
for x in range(10):
  print(x)
else:
  print("Finally finished!")
```
# 元组
## 概念
元组:
python内置的数据结构之一
是一个不可变列表（没有增、删、改的操作）  

## 创建元组  
- 使用括号()：``t=(s1,s2)``
  - 也可以省略括号，如：``t=s1,s2``
- 使用内置函数tuple()，如：``t = tuple((s1,s2))``，**注意是两层括号**
- ``range()``函数：``t=tuple(range(1,6))``
- 只包含一个元组的元素需要使用小括号和逗号，例如``t=(s1,)``
```py
# 是元组
thistuple = ("apple",)
print(type(thistuple))

# 不是元组
thistuple = ("apple")
print(type(thistuple))
```
- 空元组：``()``
## 访问元组
- 索引号
  - 负索引
- 索引范围，返回值将是带有指定项目的新元组
```py
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[2:5])
# 输出：('cherry', 'orange', 'kiwi')
```
## 更改元组值
- 元组创建后将无法更改值。元组是不可变的(恒定的)。
- 但有一种方法:将元组转换为列表，更改列表，再将列表转换回元组
```py
x = ("apple", "banana", "cherry")
y = list(x)
y[1] = "kiwi"
x = tuple(y)

print(x)
```
## 元组方法
- count()：返回元组中指定值出现的次数
- index()：在元组中搜索指定的值并返回它被找到的位置
## 其他
- 遍历：``for``
- 检查项目是否存在：``in``
- 长度：``len``
- 不能删除项目，但可以完全删除元组
- 合并：直接使用``+``
# 字典
字典是一个无序、可变和有索引的集合。用花括号编写，拥有键(key)和值(value)。
## 创建字典
```py
thisdict =	{
  "brand": "Porsche",
  "model": "911",
  "year": 1963
}
print(thisdict)
```
## 访问项目
- 在方括号内引用其键名来访问字典的项目：
```py
x = thisdict["model"]
# 输出：911
```
- ``get()``
```py
x = thisdict.get("model")
```
## 更改值
- 引用键名
```py
thisdict["model"]=111
```
## 遍历字典
- 返回值是字典的键
- 逐个打印字典中的所有键名:
```py
for x in thisdict:
    print(x)
```
- 逐个打印字典中的所有值
```py
for x in thisdict:
  print(thisdict[x])
```
- 利用``values()``返回字典的值
```py
for x in thisdict.values():
  print(x)
```
- 使用``items()``遍历键和值
```py
for x, y in thisdict.items():
  print(x, y)
```
## 添加项目
使用新的索引键并为其赋值
```py
thisdict["color"] = "red"
```
## 删除项目
- 方法1：``pop(指定键名)``
``thisdict.pop("model")``
- 方法2：``popitem()``删除最后插入的项目
- 方法3：``del`` 删除具有指定键名的项目
  - ``del thisdict["model"]``
  - del删除整个字典 ``del thisdict``
## 复制字典
- 不能通过 ``dict2 = dict1`` 复制字典，因为：``dict2`` 只是对 ``dict1`` 的引用，而 ``dict1`` 中的更改也将自动在 ``dict2`` 中进行
- 使用 ``copy()`` 方法来复制字典
```py
mydict = thisdict.copy()
```
- 使用 ``dict()`` 方法创建字典的副本
```py
mydict = dict(thisdict)
```
- ``dict()``构造函数
```py
thisdict = dict(brand="Porsche", model="911", year=1963)
# 请注意，关键字不是字符串字面量
# 请注意，使用了等号而不是冒号来赋值
print(thisdict)
```
## 字典方法
```py
clear()	# 删除字典中的所有元素
copy() #返回字典的副本
fromkeys()	# 返回拥有指定键和值的字典
get() # 返回指定键的值
items()	# 返回包含每个键值对的元组的列表
keys() # 返回包含字典键的列表
pop() # 删除拥有指定键的元素
popitem() # 删除最后插入的键值对
setdefault() # 返回指定键的值。如果该键不存在，则插入具有指定值的键。
update() # 使用指定的键值对字典进行更新
values() # 返回字典中所有值的列表
```
## 其他
- 检查键是否存在：``in`` 
```py
if "model" in thisdict:
  print("Yes, 'model' is one of the keys in the thisdict dictionary")
```
- 字典长度 ``len``
- 嵌套字典
```py
# 创建包含三个字典的字典
myfamily = {
  "child1" : {
    "name" : "Phoebe Adele",
    "year" : 2002
  },
  "child2" : {
    "name" : "Jennifer Katharine",
    "year" : 1996
  },
  "child3" : {
    "name" : "Rory John",
    "year" : 1999
  }
}
for i in myfamily.keys():
    child_name=myfamily[i]['name']
    child_year=myfamily[i]['year']
    print(f"{i}'s name is {chile_name}, and his or her was born in {child_year}.")
# 嵌套三个已经作为字典存在的字典
child1 = {
  "name" : "Phoebe Adele",
  "year" : 2002
}
child2 = {
  "name" : "Jennifer Katharine",
  "year" : 1996
}
child3 = {
  "name" : "Rory John",
  "year" : 1999
}

myfamily = {
  "child1" : child1,
  "child2" : child2,
  "child3" : child3
}
```
## zip()函数
zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。

如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。
```py
a = [1,2,3]
b = [4,5,6]
c = [4,5,6,7,8]
zipped = zip(a,b) # 返回一个对象
list(zipped) # list() 转换为列表
# [(1, 4), (2, 5), (3, 6)]
list(zip(a,c)) # 元素个数与最短的列表一致
# [(1, 4), (2, 5), (3, 6)]
a1, a2 ==zip(*zip(a,b))  # 与 zip 相反，zip(*) 可理解为解压，返回二维矩阵式
list(a1) 
# [1, 2, 3]
list(a2) 
# [4, 5, 6]
```
# 函数
## 创建函数
``def``关键字定义函数
```py
def my_function():
  print("Hello from a function")
```
## 调用
### 参数
- 默认参数值
```py
def my_function(country = "China"):
  print("I am from " + country)

my_function("Sweden") # I am from Sweden
my_function("India") # I am from India
my_function() # I am from China 
```
- 以 List 传参
参数可以是任何数据类型（字符串、数字、列表、字典等），并且在函数内其将被视为相同数据类型
```py
def my_function(food):
  for x in food:
    print(x)

fruits = ["apple", "banana", "cherry"]

my_function(fruits)
```
### 返回值
### 关键字参数 ``key=value``
```py
def my_function(child3, child2, child1):
  print("The youngest child is " + child3)

my_function(child1 = "Phoebe", child2 = "Jennifer", child3 = "Rory")
```
### 任意参数
不知道将传递给函数多少个参数，在函数定义的参数名称前添加``*``。
## 递归