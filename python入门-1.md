---
title: python入门-1
date: 2023-01-29 12:33:24
tags: python
---
# python入门-1
# Directory
- 输入输出
  - 输出
    - 字符串
    - 格式化
    - 浮点数
  - 输入
- 列表
  - 索引
  - 遍历
  - 内置函数
  - 合并列表
  - 切片
- 运算符
<!-- more -->
# 输入输出
## 输出
### 输出字符串
- 成对的单引号
```py
print('Hello World!')
```
- 三对单引号
```py
print('''Hello World!''')
```
- 一对双引号
```py
print("Hello World!")
```
- 三对双引号
```py
print("""Hello World!""")
```
- 存储到变量中再输出
```py
str='Hello World!'
print(str)
```
#### 字符串其他
- 字符串拼接直接``+``
- ``len()``获取长度
- 大小写转换
```py
.lower() --- 全部小写
.upper() --- 全部大写
.title() --- 各个字符的首字母大写
.capitalize() --- 首字母大写
.swapcase()---大小写对调
```
- 字符串搜索
```py
text.count("o")#搜索并统计"o"出现的次数
text.count("o",28)#搜索并统计，从第28位开始，"o"出现的次数
text.startswith("only")#text以"only"开通
text.startswith("only",2,10)#text的第3-9个字符以"only"开通
text.find("you")#查找you 未找到返回-1
text='I like bananas' text.replace("bananas","apples")# 替换 输出I like apples
```
- 空格
```py
.strip() --- 删除两边空格
.lstrip() --- 删除左边空格
.rstrip() --- 删除右边空格
.replace(" ","") --- 删除所有空格
.split() --- 先切分，"".join() --- 再拼接
# s=' hello wo r ld   '
# a=s.split(' ')
# print(''.join(a))
```
- split()函数
讲字符串按照特定的字符拆分成列表
```py
str1="a|b|c"
str2=str1.split("|")
print(str2)
# 输出['a','b','c']
```
- 截取字符串前10位
方法一：
```py
a = input()
if len(a) >= 10:
    print(a[0:10])
# 左闭右开
```
方法二：
```py
print(input()[0:10])
```
方法三：
```py
str = input()
for i in range(10):
    print (str[i],end='')
```
方法四：
```py
str1 = input()
print('%.10s'%str1)
```
方法五：
```py
a=input()
b=''
n=0
for i in a:
    b=b+i
    n+=1
    if n>=10:
        break
print(b)
```
方法六（slice函数法）：
```py
str1=input()
print(str1[slice(10)])
```
方法七：
```py
str = input()
if len(str) < 10 :
    exit(0)
print(str[0:10])
```
方法八：
```py
a=input('')
b=[]
for i in range(10):
    b.append(a[i])
    # append：在列表ls最后(末尾)添加一个元素object
    # 语法：ls.append(object) 
    # 无返回值
    # object 可以添加 列表，字典，元组，集合，字符串等。
s=''.join(b)
print(s)
```
方法九：
```py
a=str(input())
while len(a)>=10:
    print(a[0:10])
    break
```
- ASCII
  - ``ord()``返回单个字符的ASCII值(0-255)
  - ``chr()``输入一个整数(0-255)返回对应的ASCII符号
#### 处理引号冲突的四种办法
- 方法一：用转义字符
转义字符 反斜杠\，使 '被认为是一个字符
```py
print('Let\'s go')
```
- 方法二：单双引号交叉使用
也就是说如果字符串本身含有单引号，那么字符串两端就用双引号来标记，反之亦然
```py
print( "Let's go")
```
开头和结尾成对出现的双引号，定义了这个字符串，而其中的‘ 则被认为是字符串中的一个字符
- 方法三：三引号
虽然三引号被用来定义多行文本，但是同样可以用来定义单行文本，当使用三引号标记字符串时，那么字符串本身的单引号和双引号都能正常显示，
```py
print('''Lilei said,"Let's go!"''')
# 输出：Lilei said,"Let's go!"
```
- 方法四：Ascii码
```py
print('Lilei said,%cLet%cs go!%c' % (34,39,34))
```
#### 多行输出
- 方法1：多个print
```py
print(str1)
print(str2)
```
- 方法2：sep参数

设置输出的多个对象之间连接的符号，一般在print语句中会输出多个参数，不写则默认是按照空格连接
```py
print(str1,str2,sep("\n"))
# 用换行连接参数
```
  - 注意：end参数
    - 输出的内容以什么结尾
    - 不写则默认是以换行符结尾
    - 格式：print(.., end="某字符")
- 方法3：字符串拼接
```py
print(str1+"\n"+str2)
```
### 格式化输出
- 方法1：字典
```py
names={"Niuniu":["I am Niuniu and I am studying Python in Nowcoder!"],
       "Niumei":["I am Niuniu and I am studying Python in Nowcoder!"],
       "Niuke":["I am Niuke and I am studying Python in Nowcoder!"]
       ｝
name=input()
for i in names:#遍历字典
    if name==i:#遍历字典获取key,通过key和输入的值判断
        print(names[name])
```
- 方法2：f-string
```py
name = input()
print(f'I am {name} and I am studying Python in Nowcoder!')
```
- 方法3：format()
```py
name = input()
print('I am {} and I am studying Python in Nowcoder!'.format(name)) 
```
- 方法4：%格式化
```py
name = input()
print('I am {} and I am studying Python in Nowcoder!'.%name) 
```
### 浮点数输出的位数
- 方法1：round()
  - 语法：round(x,n)
  - x:浮点数，n:保留的小数位数
  - 不写参数则默认不保留小数
  - 注：会抹零！慎用

- 方法2：利用"%.nf"输出n位小数
```py
a=float(input())
print('%.2f' % a)
```
- 方法3：format函数
  - 使用一个大括号表示需要填充的参数
  - ``:``后面可以规定数字的精度与类型
```py
print("{:.2f}".format(3.1415926)) 
# 3.14
```
- 方法4：``f"{:.nf}"``
```py
a=float(input())
print(f"{a:.2f}")
```
### 其他
- ``type()``输出类型
```py
num=1
print(type(num))
# 输出：<class 'int'>
```
- 强制类型转换
```py
n=int(float(input()))
print(n)
# 输入1.6 输出1
# 向下取值
```
```py
n=float(int(input()))
print(n,type(n),sep='\n')
# 输入1
# 输出1.0
#    <class 'float'>
```
- int(x,base=10)
  - x -- 字符串或数字
  - base -- 进制数，默认十进制。
```py
int('12',16) # 如果带参数base，要以字符串的形式进行输入，12为16进制18  
# 输出18
int('0xa',16) # 16进制 转10进制
# 输出10  
```
## 输入
- ``input()``函数接受一个标准输入数据，返回为 string 类型
- 统一行输入多个整数，需要映射``x,y,z=map(int,input().split())``
- 输入一行整数，转换成列表``num_list=list(map(int,input().split(" ")))``
# list列表
## 索引
- 正索引 第一项的索引为0
- 负索引 -1表示最后一项，-2表示倒数第二项...
- 索引范围：``list[a,b]``讲从a(包括)开始，到b(不包括)结束
  - ``list[-4:-1]``将返回从索引 -4(包括)到索引 -1(排除)的项目
- 更改项目值，直接引用索引号：``list[1]=new value``更改第二项
## 遍历列表
- 遍历列表
```py
list=['a','b','c']
for x in list:
    print(x)
```
- 检查项目是否存在``in``
```py
thislist = ["apple", "banana", "cherry"]
if "apple" in thislist:
  print("Yes, 'apple' is in the fruits list")
```
- 判断列表是否为空
  - 方法1：``if(len(mylist==0))``
  - 方法2：``if mylist`` ``if not mylist``
## list常见的内置函数
```py
len() # 求列表元素个数
max() # 求列表最大值
min() # 求列表最小值
sum() # 求列表的和
reverse() # 颠倒列表的顺序
sorted() # 求排序后的列表序列
# list1=[1,3,2]
# print(sorted(list1))临时排序
# list1.sort() 升序
# list1.sort(reverse=True) 降序
# print(list1) 改变list1
list() # 将其他数据结构转换成列表
any() # 只要列表里有一个True就会返回True
all() # 表里的所有元素都是True才会返回True
append() # 将项目添加到列表的末尾
insert() # 在指定的索引处添加项目
# thislist = ["apple", "banana", "cherry"]
# thislist.insert(1, "orange")
# print(thislist)
index()	# 返回具有指定值的第一个元素的索引
remove() # 删除指定的项目
pop() # 删除指定的索引(未指定索引则删除最后一项)
del mylist[i]# 删除指定的索引
del mylist # 完整删除列表
clear() # 清空列表
newlist=oldlist.copy() # 复制列表
newlist=list(oldlist) # 复制列表
```
## 合并列表
- 方法1：``+``
```py
newlist = list1 + list2 # 合并列表
```
- 方法2：追加append()
```py
list1 = ["a", "b" , "c"]
list2 = [1, 2, 3]
for x in list2:
  list1.append(x)
print(list1)
```
- 方法3：追加exend()
```py
list1 = ["a", "b" , "c"]
list2 = [1, 2, 3]

list1.extend(list2)
print(list1)
```
- 注：列表可以存放列表
## 切片
- slice切片函数: 第一个参数-start index 第二个参数-end index,第三个参数为step间距(可省略)
- 未指定索引：
  - 未指定第一个索引，默认从表头(可以是从左到右的,也可以是从右到左的,看step的正负情况)开始
  - 未指定最后一个索引，默认从表尾(可以是从左到右的,也可以是从右到左的,看step的正负情况)结束,即为len(list)
- 未指定步长:
  - 默认步长值为 1;
  - 步长<0, 则从右→左
  - 步长>0,则从左→右
```py
print(group_list[:2])    # 也可以写成: print(group_list[0:2])
print(group_list[1:4:])  # 也可以写成: print(group_list[1:4])
print(group_list[3::])   # 也可以写成: print(group_list[-2:]) 或 print(group_list[3:])
```
# 运算符
- 算术运算符
  - ``+`` 加
  - ``-`` 减
  - ``*`` 乘
  - ``/`` 除
  - ``//`` 地板除（取整）
  - ``**``幂
  - ``==``返回值是true或者false
- 赋值运算符
  - ``=``
  - ``=``的衍生，如：``+=`` ``-=`` ``*=``
- 比较运算符
  - ``=`` ``!=``
  - ``>`` ``<`` ``>=`` ``<=``
- 逻辑运算符
  - ``and``
  - ``or``
  - ``not``
- 身份运算符
  - ``is``
  - ``is not``
- 成员运算符
  - ``in``
  - ``not in``
- 位运算符
  - ``&`` and
  - ``|`` or
  - ``^`` xor
  - ``~`` not
  - ``<<`` left shift
  - ``>>`` right shift