---
title: c++_review_basis
date: 2023-01-30 17:24:35
tags: c++
---
# Directory
- 综述
- 环境设置
- 基本语法
- 数据类型
- 变量 & 常量
- 函数
- 数学
- 数组
- 字符串
- 引用
- 日期和时间
- 输入输出
- 数据结构（结构体）
<!-- more -->
# 综述
## 面向对象程序设计
面向对象开发的四大特性：
- 封装
- 抽象
- 继承
- 多态
## 标准库
C++的组成部分
- 核心语言
- c++标准库
- 标准模板库(STL)
## 历史
- 1998 c++98
- 2003 c++03
- 2011 c++11
- 2014 c++14
- 2017 c++17
- 2020 c++20
# 环境设置
## 文本编辑器：
Windows Notepad(Windows)、OS Edit command、Brief、Epsilon、EMACS 和 vim/vi(Windows 和 Linux/UNIX)
## c++编译器：
把源代码编译成最终的可执行程序，GNU 的 C/C++ 编译器是最常用的免费编译器。
- windows上安装GCC需要安装MinGW
- GNU工具： gcc、g++、ar、ranlib、dlltool等
  - 最简单的编译方式：``$ g++ helloworld.cpp``,命令行中未指定可执行程序的文件名，编译器采用默认的 a.out，故同样可以这样运行``$ ./a.out``
  - 使用 ``-o`` 指定可执行程序的文件名，``$ g++ helloworld.cpp -o helloworld``，执行 helloworld:``$ ./helloworld``
  - 多个 C++ 代码文件，``$ g++ runoob1.cpp runoob2.cpp -o runoob``生成一个 runoob 可执行文件
- g++常用命令选项
```c++
-ansi   //只支持 ANSI 标准的 C 语法。这一选项将禁止 GNU C 的某些特色， 例如 asm 或 typeof 关键词。
-c	//只编译并生成目标文件。
-DMACRO	//以字符串"1"定义 MACRO 宏。
-DMACRO=DEFN //以字符串"DEFN"定义 MACRO 宏。
-E //只运行 C 预编译器。
-g //生成调试信息。GNU 调试器可利用该信息。
-IDIRECTORY	//指定额外的头文件搜索路径DIRECTORY。
-LDIRECTORY	//指定额外的函数库搜索路径DIRECTORY。
-lLIBRARY	//连接时搜索指定的函数库LIBRARY。
-m486	//针对 486 进行代码优化。
-o	//FILE 生成指定的输出文件。用在生成可执行文件时。
-O0	//不进行优化处理。
-O	//或 -O1 优化生成代码。
-O2	//进一步优化。
-O3	//比 -O2 更进一步优化，包括 inline 函数。
-shared	//生成共享目标文件。通常用在建立共享库时。
-static	//禁止使用共享连接。
-UMACRO	//取消对 MACRO 宏的定义。
-w	//不生成任何警告信息。
-Wall	//生成所有警告信息。
```
## makefile
# 基本语法
- 头文件：包含程序中必需的有用的信息
- ``using namespace std``：使用std命名空间
- ``main()``是程序开始执行的地方
- ``return 0``终止main函数，向调用进程返回值0
- ``;`` 语句结束符
- ``{}`` 语句块
- c++保留字
- 三字符组
# 数据类型
- 7种基本类型：bool, char, int, float, double, void, wchar_t(宽字符型，``typedef short int wchar_t;``)
- 类型修饰符:signed, unsigned, short, long
- ``typedef``  为一个已有的**类型**取一个新的名字：``typedef int feet;feet distance;``
- 枚举类型``enum``
```cpp
#include<iostream>
using namespace std;
enum color{ //枚举名
    red,
    green=5,// 标识符[=整型常数]
    blue
};
int main()
{
    cout<<color::red<<endl;// 第一个名称默认值为0
    color c=blue; // c: 定义枚举变量
    cout<<c<<endl; // 默认每个名称比前面一个名称大 1
}
```
## 左值右值
- 左值（lvalue）：指向内存位置的表达式被称为左值（lvalue）表达式。左值可以出现在赋值号的左边或右边。**变量是左值**。
- 右值（rvalue）：术语右值（rvalue）指的是存储在内存中某些地址的数值。右值是不能对其进行赋值的表达式，也就是说，右值可以出现在赋值号的右边，但不能出现在赋值号的左边。**数值型的字面值是右值**。
# 变量 & 常量
## 变量
### 变量作用域
定义变量的三个地方
- 局部变量
- 形式参数
- 全局变量
## 常量
### 整数常量
- 前缀：指定基数：默认表示十进制，0x 或 0X 表示十六进制，0 表示八进制。
- 后缀：后缀是 U 和 L 的组合，不要求大小写。
  - U(unsigned) ：无符号整数
  - L(long) : 长整数
### 浮点常量
- 浮点常量由整数部分、小数点、小数部分和指数部分组成
- 表示浮点常量
  - 小数形式
  - 指数形式
    - 必须包含小数点、指数，或同时包含两者。带符号的指数用 e 或 E 引入的
### 布尔常量
- true 1 
- false 0
### 字符常量
- 字符常量括在单引号中
- 如果常量以 ``L``（仅当大写时）开头，则表示是一个宽字符常量（例如 ``L'x'``），此时它必须存储在 ``wchar_t`` 类型的变量中。否则，它就是一个窄字符常量（例如 ``'x'``），此时它可以存储在 ``char`` 类型的简单变量中。

- 字符常量可以是一个普通的字符（例如 ``'x'``）、一个转义序列（例如 ``'\t'``），或一个通用的字符（例如`` '\u02C0'``）。

- 转义字符：一些特定的字符，前面有反斜杠就具有特殊的含义。
### 字符串常量
- 字符串字面值或常量是括在双引号 "" 中
## 定义常量
- 使用 ``#define`` 预处理器: ``#define LENGTH 10 ``
- 使用 ``const`` 关键字：``const int  LENGTH = 10;``
- 注：把常量定义为大写字母形式，是一个很好的习惯
## 修饰符类型
数据类型修饰符：
- signed 整型 字符型 前缀
- unsigned 整型 字符型 前缀
- long 整型 双精度型
- short 整型
## 类型限定符
```
const       //const 类型的对象在程序执行期间不能被修改改变。
volatile    //修饰符 volatile 告诉编译器不需要优化volatile声明的变量，让程序可以直接从内存中读取变量。对于一般的变量编译器会对变量进行优化，将内存中的变量值放在寄存器中以加快读写效率。
restrict    //由 restrict 修饰的指针是唯一一种访问它所指向的对象的方式。只有 C99 增加了新的类型限定符 restrict。
```
# 存储类
存储类定义 C++ 程序中变量/函数的范围（可见性）和生命周期
- auto
  - 根据初始化表达式自动推断该变量的类型
  - 声明函数时函数返回值的占位符
```cpp
auto f=3.14;      //double
auto s("hello");  //const char*
auto z = new auto(9); // int*
auto x1 = 5, x2 = 5.0, x3='r';//错误，必须是初始化为同一类型
```
- register
  - `` register int  miles;``
  - 定义存储在寄存器中而不是 RAM 中的局部变量。
  - 寄存器只用于需要快速访问的变量，比如计数器
  - 变量的最大尺寸等于寄存器的大小（通常是一个词）
  - 且不能对它应用一元的 '&' 运算符（因为它没有内存位置）
- static
  - ``static int i = 5; // 局部静态变量``
  - 指示编译器在程序的生命周期内保持局部变量的存在，而不需要在每次它进入和离开作用域时进行创建和销毁。因此，使用 static 修饰局部变量可以在函数调用之间保持局部变量的值。
  - static 修饰符也可以应用于全局变量。当 static 修饰全局变量时，会使变量的作用域限制在声明它的文件内。
  - 在 C++ 中，当 static 用在类数据成员上时，会导致仅有一个该成员的副本被类的所有对象共享。
- extern
  - 用于提供一个全局变量的引用，全局变量对所有的程序文件都是可见的。当使用 'extern' 时，对于无法初始化的变量，会把变量名指向一个之前定义过的存储位置。
  - 有多个文件且定义了一个可以在其他文件中使用的全局变量或函数时，可以在其他文件中使用 extern 来得到已定义的变量或函数的引用。可以这么理解，extern 是用来在另一个文件中声明一个全局变量或函数。
  - extern 修饰符通常用于当有两个或多个文件共享相同的全局变量或函数的时候

例：
```cpp
#include <iostream>
 
int count ;
extern void write_extern();
 
int main()
{
   count = 5;
   write_extern();
}
```
```cpp
#include <iostream>
 
extern int count;
 
void write_extern(void)
{
   std::cout << "Count is " << count << std::endl;
}
```
``$ g++ main.cpp support.cpp -o write``
```cpp
$ ./write
Count is 5
```
- mutable
  - 仅适用于类的对象
  - 允许对象的成员替代常量。也就是说，mutable 成员可以通过 const 成员函数修改。
- thread_local (C++11)
  - 声明的变量仅可在它在其上创建的线程上访问。 
  - 变量在创建线程时创建，并在销毁线程时销毁。 
  - 每个线程都有其自己的变量副本。
  - 仅应用于数据声明和定义
  - 不能用于函数声明或定义
# 运算符
- 算术运算符
- 关系运算符
- 逻辑运算符
- 位运算符
- 赋值运算符
- 杂项运算符
  - sizeof
  - ``Condition ? x : y`` 条件运算符，如果 Condition 为真 ? 则值为 X : 否则值为 Y
  - ``,`` 逗号运算符会顺序执行一系列运算。整个逗号表达式的值是以逗号分隔的列表中的最后一个表达式的值。
  - ``.`` ``->`` 成员运算符用于引用类、结构和共用体的成员
  - cast：强制转换运算符，``int(2.2)``
  - ``&``
  - ``*`` 指针运算符，指向一个变量，``*var`` 指向变量 ``var``
# 循环
- ``while``
- ``for``
- ``do...while``
- 无限循环 ``for( ; ; )``
# 判断
- if else
- 条件运算符 ``Exp1 ? Exp2 : Exp3;`` 和if else等价
- ``switch``
```cpp
switch(expression){ // expression 必须是一个整型或枚举类型，或者是一个 class 类型，其中 class 有一个单一的转换函数将其转换为整型或枚举类型。
    case constant-expression  :
       statement(s);
       break; // 可选的 当遇到 break 语句时，switch 终止，控制流将跳转到 switch 语句后的下一行。
    case constant-expression  :
       statement(s);
       break; // 可选的 当遇到 break 语句时，switch 终止，控制流将跳转到 switch 语句后的下一行。
  
    // 您可以有任意数量的 case 语句
    default : // 可选的 default case 可用于在上面所有 case 都不为真时执行一个任务
       statement(s);
}
```
# 函数
- 定义
- 声明
- 调用
- 三种参数传递方式
  - **传值调用** 修改形参不影响实参
  - **指针调用** 修改形参影响实参
  - **引用调用** 修改形参影响实参
## lambda函数 
- Lambda函数（Lambda表达式）也叫做匿名函数
- Lambda表达式把函数看作对象，比如：可以将它们赋给变量和作为参数传递，也可以像函数一样求值
```cpp
[capture](parameters)->return-type{body}
//例如
[](int x, int y){ return x < y ; }
//返回类型可以被明确的指定
[](int x, int y) -> int { int z = x + y; return z + x; }
```
```cpp
[]      // 沒有定义任何变量。使用未定义变量会引发错误。
[x, &y] // x以传值方式传入（默认），y以引用方式传入。
[&]     // 任何被使用到的外部变量都隐式地以引用方式加以引用。
[=]     // 任何被使用到的外部变量都隐式地以传值方式加以引用。
[&, x]  // x显式地以传值方式加以引用。其余变量以引用方式加以引用。
[=, &z] // z显式地以引用方式加以引用。其余变量以传值方式加以引用
```
- 另外有一点需要注意。对于``[=]``或``[&]``的形式，``lambda`` 表达式可以直接使用 ``this`` 指针。但是，对于``[]``的形式，如果要使用 ``this`` 指针，必须显式传入
```cpp
[this]() { this->someFunc(); }();
```
# 数学
## 数学运算
头文件``<cmath>``
```cpp
序号	函数 & 描述
1	double cos(double); //返回double 型弧度角的余弦
2	double sin(double);//返回double 型弧度角的正弦
3	double tan(double);//返回double 型弧度角的正切
4	double log(double);//返回参数的自然对数
5	double pow(double, double);//返回 x 的 y 次方
6	double hypot(double, double);//返回两个参数的平方和的平方根
7	double sqrt(double);//返回参数的平方根。
8	int abs(int);//返回整数的绝对值。
9	double fabs(double);//返回任意一个浮点数的绝对值
10	double floor(double);//返回一个小数向下取整
11  double ceil(double);//返回一个小数向上取整
12  double round(double);//返回一个小数四舍五入
```
## 随机数
头文件``<cstdlib>``
-  伪随机数,每次执行时是相同的; 若要不同,需要用函数srand()初始化
  - ``rand()`` 是根据一个数（种子）为基准以某个递推公式推算出来的一系列数，当这系列数很大的时候，就符合正态公布，从而相当于产生了随机数，但这不是真正的随机数
- ``srand()`` 
  - ``void srand(unsigned int seed);``
  - 参数seed必须是个整数，通常利用time(0)的返回值或NULL来当做seed
  - 因为调用时间通常不一样，所以通过调用时间函数保证随机性
  - 如果每次seed都设相同值，rand()所产生的随机数值每次就会一样。
```cpp
(rand() % (b-a))+ a --> [a,b)
(rand() % (b-a+1))+ a --> [a,b]
(rand() % (b-a))+ a + 1 --> (a,b]
```
```cpp
#include <iostream>
#include <ctime>
/*
time()函数返回格林尼治时间1970年1月1日00:00:00到当前时刻的时长，时长单位是秒
time(0)函数返回当前格林尼治标准时间与格林尼治标准时间1970年0分0秒的时间间隔
*/
#include <cstdlib>//随机数头文件
 
using namespace std;
 
int main ()
{
   int i,j;
   srand( (unsigned)time( NULL ) );// 设置种子
   for( i = 0; i < 10; i++ )// 生成 10 个随机数
   {
      j= rand();// 生成实际的随机数
      cout <<"随机数： " << j << endl;
   }
   return 0;
}
```
# 数组
## 指向数组的指针
```cpp
double runoobAarray[5] = {1000.0, 2.0, 3.4, 17.0, 50.0};
//runoobAarray 是一个指向 &runoobAarray[0] 的指针，即数组 runoobAarray 的第一个元素的地址
double *p;
p = runoobAarray;
//把 p 赋值为 runoobAarray 的第一个元素的地址
//使用数组名作为常量指针是合法的。
//因此，*(runoobAarray + 4) 是一种访问 runoobAarray[4] 数据的合法方式。
//把第一个元素的地址存储在 p 中，可以使用 *p、*(p+1)、*(p+2) 等来访问数组元素

// 输出数组中每个元素的值
cout << "使用指针的数组值 " << endl; 
for ( int i = 0; i < 5; i++ )
{
    cout << "*(p + " << i << ") : ";
    cout << *(p + i) << endl;
}
/*
使用指针的数组值
*(p + 0) : 1000
*(p + 1) : 2
*(p + 2) : 3.4
*(p + 3) : 17
*(p + 4) : 50
*/

cout << "使用 runoobAarray 作为地址的数组值 " << endl;
for ( int i = 0; i < 5; i++ )
{
    cout << "*(runoobAarray + " << i << ") : ";
    cout << *(runoobAarray + i) << endl;
}
/*
使用 runoobAarray 作为地址的数组值
*(runoobAarray + 0) : 1000
*(runoobAarray + 1) : 2
*(runoobAarray + 2) : 3.4
*(runoobAarray + 3) : 17
*(runoobAarray + 4) : 50
*/
```
## 传递数组给函数
- 可以通过指定不带索引的数组名来传递一个指向数组的指针。
- 传数组给一个函数，数据类型自动转换为指针类型，因而传的实际是地址。
- 传递一维数组作为参数有以下三种方式来声明函数形式参数。(这三种声明方式的结果是一样的，因为每种方式都会告诉编译器将要接收一个整型指针。)
- 方式1：形式参数是一个指针 ``void myFunction(int *param)``
- 方式2：形式参数是一个已定义大小的数组 ``void myFunction(int param[10])``
- 方式3：形式参数是一个未定义大小的数组 ``void myFunction(int param[])``
## 从函数返回数组
- C++ 不允许返回一个完整的数组作为函数的参数。
- 但可以通过指定不带索引的数组名来返回一个指向数组的指针。
- 从函数返回一个一维数组必须声明一个**返回指针的函数**
```cpp
int * myFunction()
```
实例：生成 10 个随机数，并使用数组来返回它们
```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
 
using namespace std;

int * getRandom( )// 要生成和返回随机数的函数
{
  static int  r[10];
  srand((unsigned)time(0));// 设置种子
  for (int i = 0; i < 10; ++i)
  {
    r[i] = rand();
    cout << r[i] << endl;
  }
  return r;
}

int main ()
{
   int *p; // 一个指向整数的指针
   p = getRandom();
   for ( int i = 0; i < 10; i++ )
   {
       cout << "*(p + " << i << ") : "<< *(p + i) << endl;
   }
   return 0;
}
```
# 字符串 ``char *``
- C++ 编译器会在初始化数组时，自动把 \0 放在字符串的末尾
## 字符串函数
```cpp
序号    函数 & 目的
1   strcpy(s1, s2); //复制字符串 s2 到字符串 s1
2   strcat(s1, s2); //连接字符串 s2 到字符串 s1 的末尾
//连接字符串也可以用 + 号，例如:
// string str1 = "runoob";
// string str2 = "google";
// string str = str1 + str2;
3   strlen(s1); //返回字符串 s1 的长度
4   strcmp(s1, s2); //如果 s1==s2 返回 0；
                    //如果 s1<s2 返回值小于0
                    //如果 s1>s2 返回值大于0
5   strchr(s1, ch); //返回一个指针，指向字符串 s1 中字符 ch 的第一次出现的位置。
6   strstr(s1, s2); //返回一个指针，指向字符串 s1 中字符串 s2 的第一次出现的位置。
```
# 指针
## 指针声明
指针是一个变量，其值为另一个变量的地址，即，内存位置的直接地址。
```cpp
int    *ip;    /* 一个整型的指针 */
double *dp;    /* 一个 double 型的指针 */
float  *fp;    /* 一个浮点型的指针 */
char   *ch;    /* 一个字符型的指针 */
```
## 指向指针的指针(多级间接寻址)
```cpp
int  var = 3000;
int  *ptr;
int  **pptr;

// 获取 var 的地址
ptr = &var;
// 使用运算符 & 获取 ptr 的地址
pptr = &ptr;

// 使用 pptr 获取值
cout << "var 值为 :" << var << endl;//3000
cout << "*ptr 值为:" << *ptr << endl;//3000
cout << "**pptr 值为:" << **pptr << endl;//3000
```
# 引用
## 引用 vs 指针
三个主要的不同：
- 不存在空引用。引用必须连接到一块合法的内存。
- 一旦引用被初始化为一个对象，就不能被指向到另一个对象。指针可以在任何时候指向到另一个对象。
- 引用必须在创建时被初始化。指针可以在任何时间被初始化。
## 创建引用
```cpp
int i = 17;
int& r = i; // r 是一个初始化为 i 的整型引用
double& s = d; // s 是一个初始化为 d 的 double 型引用
```
## 把引用作为返回值
- 通过使用引用来替代指针，会使程序更容易阅读和维护。
- 函数可以返回一个引用，方式与返回一个指针类似。
- 当函数返回一个引用时，则返回一个指向返回值的隐式指针。这样，函数就可以放在赋值语句的左边。
# 日期和时间
头文件``<ctime>``
- clock_t
- time_t
- size_t
- tm 把日期和时间以 C 结构的形式保存，tm 结构的定义如下：
```cpp
struct tm {
  int tm_sec;   // 秒，正常范围从 0 到 59，但允许至 61
  int tm_min;   // 分，范围从 0 到 59
  int tm_hour;  // 小时，范围从 0 到 23
  int tm_mday;  // 一月中的第几天，范围从 1 到 31
  int tm_mon;   // 月，范围从 0 到 11
  int tm_year;  // 自 1900 年起的年数
  int tm_wday;  // 一周中的第几天，范围从 0 到 6，从星期日算起
  int tm_yday;  // 一年中的第几天，范围从 0 到 365，从 1 月 1 日算起
  int tm_isdst; // 夏令时
};
```
- clock_t、size_t 和 time_t 能够把系统时间和日期表示为某种整数。
```cpp
序号	函数 & 描述
1	time_t time(time_t *time); // 返回系统的当前日历时间，自 1970 年 1 月 1 日以来经过的秒数。如果系统没有时间，则返回 -1。
2	char *ctime(const time_t *time); // 返回一个表示当地时间的字符串指针，字符串形式 day month year hours:minutes:seconds year。
3	struct tm *localtime(const time_t *time); // 返回一个指向表示本地时间的 tm 结构的指针。
4	clock_t clock(void); // 返回程序执行起（一般为程序的开头），处理器时钟所使用的时间。如果时间不可用，则返回 -1。
5	char * asctime ( const struct tm * time ); // 返回一个指向字符串的指针，字符串包含了 time 所指向结构中存储的信息，返回形式为：day month date hours:minutes:seconds year\n\0。
6	struct tm *gmtime(const time_t *time); // 返回一个指向 time 的指针，time 为 tm 结构，用协调世界时（UTC）也被称为格林尼治标准时间（GMT）表示。
7	time_t mktime(struct tm *time); // 返回日历时间，相当于 time 所指向结构中存储的时间。
8	double difftime ( time_t time2, time_t time1 ); // 返回 time1 和 time2 之间相差的秒数。
9	size_t strftime(); // 用于格式化日期和时间为指定的格式。
```
# 输入输出
- I/O 发生在流中，流是字节序列。
- 输入：字节流从设备（如键盘、磁盘驱动器、网络连接等）流向内存
- 输出：字节流从内存流向设备（如显示屏、打印机、磁盘驱动器、网络连接等）
## I/O 库头文件
```cpp
头文件	        函数和描述
<iostream>  //cin 标准输入流
            //cout 标准输出流
            //cerr (非缓冲)标准错误流
            //clog 缓冲标准错误流(标准日志流)
<iomanip>   //参数化的流操纵器
            //setw
            //setprecision
<fstream>	//文件和流
```
# 数据结构
## 结构体
```
struct type_name{
    type_1 mem1;
    type_2 mem2;
}object_name;
```
- 访问结构成员``.``
- 指向结构的指针
```cpp
struct Books *struct_pointer;//struct Books结构体类型
struct_pointer = &Book1;//& 运算符放在结构名称的前面
struct_pointer->title;//使用指向该结构的指针访问结构的成员，必须使用 -> 运算符
```
- typedef 关键字
```cpp
typedef struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
}Books;

//可以直接使用 Books 来定义 Books 类型的变量，而不需要使用 struct 关键字
Books book1, book2;
//否则
struct Books book;
```