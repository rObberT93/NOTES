---
title: python入门-3
date: 2023-01-29 21:52:09
tags: python
---
# Directory
- 类
- 继承
- try-except
- 正则表达式
- lambda匿名函数
- 内置函数
<!-- more -->
# 类
类（Class）类似对象构造函数，或者是用于创建对象的“蓝图”。
## 内置 ``__init__()`` 函数
- 所有类都有一个名为 ``__init__()`` 的函数，它始终在启动类时执行。
- 每次使用类创建新对象时，都会自动调用 ``__init__()`` 函数
- 使用 ``__init__()`` 函数将值赋给对象属性，或者在创建对象时需要执行的其他操作
## 类创建
```py
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def myfunc(self):
    print("Hello my name is " + self.name)

p1 = Person("Bill", 63)
p1.myfunc()
```
## ``self``参数
- self 参数是对类的当前实例的引用，用于访问属于该类的变量。
- 它不必被命名为 self，您可以随意调用它，但它必须是类中任意函数的首个参数：``def __init__(mysillyobject, name, age):``
## 增删改查
- 修改 ``p1.age = 40``
- 删除对象属性 ``del p1.age``
- 删除对象 ``del p1``
- ``pass``
# 继承
## 概念
- 继承允许我们定义继承另一个类的所有方法和属性的类。

- 父类是继承的类，也称为基类。

- 子类是从另一个类继承的类，也称为派生类。
## 创建父类
- 任何类都可以是父类，因此语法与创建任何其他类相同
```py
# 创建一个名为 Person 的类，
# 其中包含 firstname 和 lastname 属性
# 以及 printname 方法：

class Person:
  def __init__(self, fname, lname):
    self.firstname = fname
    self.lastname = lname

  def printname(self):
    print(self.firstname, self.lastname)

# 使用 Person 来创建对象，然后执行 printname 方法：

x = Person("Bill", "Gates")
x.printname()
```
## 创建子类
```py
#创建一个名为 Student 的类，它将从 Person 类继承属性和方法
class Student(Person):
  pass # pass 表示不向该类添加任何其他属性或方法
# Student 类拥有与 Person 类相同的属性和方法
x = Student("Elon", "Musk")
x.printname()
# 使用 Student 类创建一个对象，然后执行 printname 方法
```
- 把``__init__()`` 函数添加到子类（而不是 pass 关键字）。
- 注释：每次使用类创建新对象时，都会自动调用 ``__init__()`` 函数
```py
class Student(Person):
  def __init__(self, fname, lname):
    # 添加属性等
```
### super函数
会使子类从其父继承所有方法和属性
```py
class Student(Person):
  def __init__(self, fname, lname):
    super().__init__(fname, lname)
```
- 不必使用父元素的名称，它将自动从其父元素继承方法和属性
## 添加属性
```py
# 添加 year 参数，并在创建对象时传递正确的年份：

class Student(Person):
  def __init__(self, fname, lname, year):
    super().__init__(fname, lname)
    self.graduationyear = year

x = Student("Elon", "Musk", 2019)
```
## 添加方法
```py
# 把名为 welcome 的方法添加到 Student 类：
class Student(Person):
  def __init__(self, fname, lname, year):
    super().__init__(fname, lname)
    self.graduationyear = year

  def welcome(self):
    print("Welcome", self.firstname, self.lastname, "to the class of", self.graduationyear)
``` 
# try-except
## 综述
- ``try`` 块允许您测试代码块以查找错误。

- ``except`` 块允许您处理错误。

- ``finally`` 块允许您执行代码，无论``try``和 ``except``块的结果如何。
## 异常处理：
- 单个异常
当发生错误或异常时，通常会停止并生成错误消息。可以使用 try 语句处理这些异常：
```py
try:
  print(x)
# try 块将生成异常，因为 x 未定义
except:
  print("An exception occurred")
# 输出：An exception occurred
```
- 多个异常
```py
try:
  print(x)
except NameError:
  print("Variable x is not defined")
# NameError: name 'xxx' is not defined
except:
  print("Something else went wrong")
```
### Else
如果没有引发错误，可以使用 else 关键字来定义要执行的代码块：
```py
try:
  print("Hello")
except:
  print("Something went wrong")
else:
  print("Nothing went wrong")
# 输出：Nothing went wrong
```
### Finally
如果指定了 finally 块，则无论 try 块是否引发错误，都会执行 finally 块
```py
try:
  print(x)
except:
  print("Something went wrong")
finally:
  print("The 'try except' is finished")
```
注：这对于关闭对象并清理资源非常有用
```py
try:
  f = open("demofile.txt")
  f.write("Lorum Ipsum")
except:
  print("Something went wrong when writing to the file")
finally:
  f.close()
# 程序可以继续，而且不会打开文件对象
```
### 引发异常
使用 ``raise`` 关键词在条件发生时抛出（引发）异常。
```py
x = -1
if x < 0:
  raise Exception("Sorry, no numbers below zero")
```
```py
x = "hello"

if not type(x) is int:
  raise TypeError("Only integers are allowed")
```
# 正则表达式
## defination
- RegEx 或正则表达式是形成搜索模式的字符序列。

- RegEx 可用于检查字符串是否包含指定的搜索模式。
## RegEx模块
名为 re 的内置包，可用于处理正则表达式``import re``
```py
# 索字符串以查看它是否以 "China" 开头并以 "country" 结尾
import re

txt = "China is a great country"
x = re.search("^China.*country$", txt)
```
### 函数
```py
findall	# 返回包含所有匹配项的列表
search # 如果字符串中的任意位置存在匹配，则返回 Match 对象
split	# 返回在每次匹配时拆分字符串的列表
sub	# 用字符串替换一个或多个匹配项
```
## 元字符
```py
[] # 一组字符
\ # 示意特殊字符
. # 任何字符
^ # 起始于
$ # 结束于
* # 零次或多次出现
+ # 一次或多次出现
{} # 确切地指定的出现次数
| # 两者任一
() # 捕获和分组
```
## 特殊序列
```py
\A # 
\b # 
\B # 
\b # 数字
\D # 非数字
\s # 包含空白字符
\S # 不包含空白字符
\w # 包含单词字符，从a到Z的字符，从0到9的数字，和下划线——
\W # 不包含任何单词字符
\Z # 
```
## 函数
- ``re.match()``从头开始匹配,如果不是起始位置匹配成功的话，match函数的匹配结果就为none。匹配成功，re.match方法返回一个匹配的对象。
  - 语法: ``re.match(pattern,string,[flags])``
  - 参数说明：
  ``pattern``: 需要匹配的正则表达式   
  ``string``:要匹配的完整字符串   
  ``flags``:标志位(默认为0)，它可以控制正则表达式的匹配方式
    - ``re.I`` 忽略匹配时的大小写
    - ``re.M`` 多行匹配，影响 ^ 和 $
    - ``re.S`` . 默认不匹配换行，使 . 匹配包括换行在内的所有字符
    - ``re.U`` 根据Unicode字符集解析字符。这个标志影响 ``\w``,``\W``,``\b``,``\B``
  - ``span()`` 返回的元组包含了匹配的开始和结束位置
  - ``.string`` 返回传入函数的字符串
  - ``group()`` 返回匹配的字符串部分
- ``re.search()`` 搜索整个字符串，并返回第一个成功的匹配。
  - 语法：``re.search(pattern, string, flags=0)``
- ``re.findall()`` 搜索整个字符串，返回一个list
  - 语法：``re.findall(string)``
- ``re.compile()`` 用于编译正则表达式，生成一个正则表达式``(Pattern)``对象。
  - 语法：``re.compile(pattern，flags=0)``
- ``re.split()`` 将一个字符串按照正则表达式匹配的结果进行分割，返回列表类型
  - 语法：``re.split(pattern, string ,?maxsplit=0?，flags=0)``
- ``re.sub()`` 在一个字符串中替换所有匹配正则表达式的子串，返回替换后的字符串
  - 语法：``re.sub(pattern, repl, string, count=0，flags=0)``
- ``sub()``把匹配替换为指定的文本
  - 语法：``sub(被替换的字符，替换成的字符，目标字符串，count)``
```py
# 去掉所有非数字字符

import re

str1=input()
str2=re.sub('\D','',str1) # \D非数字，把非数字替换成无
print(str2)
```
指定 count 参数来控制替换次数：
```py
# 替换前两次出现：

import re

str = "China is a great country"
x = re.sub("\s", "9", str, 2)
print(x)
```
# Lambda函数
- lambda 函数是一种小的匿名函数。

- lambda 函数可接受任意数量的参数，但只能有一个表达式。
```py
# 把作为参数传入的数字加 10，然后打印结果
x = lambda a : a + 10
print(x(5))
```
```py
# 有一个带一个参数的函数定义，并且该参数将乘以未知数字：

def myfunc(n):
  return lambda a : a * n
  ```
# 内置函数
- ``hex()``10进制转16进制
- ``bin()``10进制转2进制
- ``pow(x,y)``和``x**y``等价
- ``my_list.index(xxx)``返回xxx在my_list中的下标
- ``str.isalpha()``判断字符串是否只包含字母 ``str.isdigit()``判断字符串是否只包含数字
``str.isspace()``判断字符串是否包含空格
- ``find(xxx)`` 查找字符在字符串的索引下标，未查到时，返回 -1
- ``index(xxx)`` 查找字符在字符串的索引下标，未查到时，报错``ValueError``
- ``count()``字符在字符串中出现的次数
- ``join()函数``：``'sep'.join(seq)``
  - ``sep``：分隔符，可以为空
  - ``seq``：要连接的元素序列、字符串、元组、字典
  - 返回值：一个以分隔符sep连接各个元素后生成的字符串
- ``str.replace(old str,new str)``
- ``round(float number,digit)``四舍五入
- ``eval(公式字符串)`` 只要输入的字符串是一个公式，eval()函数能够直接计算这个公式的值
- ``set()``创建集合，自动去重
- ``sorted(集合)``临时排序
- ``.span`` 返回匹配值的下标