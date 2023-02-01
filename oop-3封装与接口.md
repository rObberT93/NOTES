---
title: oop_3封装与接口
date: 2023-01-26 15:26:16
tags: c++
---
# session 1
## 1.函数重载
1.1 def：同一名称的函数，有两个以上不同的函数实现
## 2.auto关键字
- 追踪返回类型的函数
可以将函数返回类型的声明信息放到函数参数列表的后面进行声明，如：
<!-- more -->
```c++
//普通函数声明形式
	int func(char* ptr, int val);
//追踪返回类型的函数声明形式
	auto func(char* ptr, int val) -> int;
```
追踪返回类型在原本函数返回值的位置使用auto关键字
- 变量必须在定义时初始化
```c++
auto a; //错误
auto b4 = 10, b5 = 20.0, b6 = 'a’;//错误,没有推导为同一类型
```
- 参数不能被声明为auto
```c++
void func(auto a) {…} //错误
```
- auto并不是一个真正的类型。不能使用一些以类型为操作数的操作符，如``sizeof``或者``typeid``。
```c++
cout << sizeof(auto) << endl;//错误
```
- 代替变量声明
```c++
vector<string> vs; 
for (vector<string>::iterator i = vs.begin(); i != vs.end(); i++) 
```
- 在定义模板函数时，用于声明依赖模板参数的变量类型
```c++
template <typename _Tx, typename _Ty> 
void Multiply(_Tx x, _Ty y) 
{ 
	auto v = x*y; //临时变量
	std::cout << v; 
}
//使用时
Multiply(2, 3); //Multiply(int, int)
Multiply(2, 3.3); //Multiply(int, double)
```
- 结合auto和decltype，自动追踪返回类型
```c++
template <typename _Tx, typename _Ty> 
auto multiply(_Tx x, _Ty y)->decltype(x*y)
	//C++11语法，C++14可省略"->"和decltype
{ 
	return x*y; 
}
//使用时
auto a = multiply(2, 3.3); //a=6.6
```
## 3.decltype
- decltype可以对变量或表达式结果的类型进行推导
重用匿名类型
```c++
struct { 
    int d;
    double b; 
}anon_s; //没有名字的结构体，定义了一个变量
int main() {
    decltype(anon_s) as ;
    //定义了一个上面匿名的结构体...
}
```
- 结合auto和decltype，自动追踪返回类型


```c++
//可以推导返回类型（C++11）
auto func(int x, int y) -> decltype(x+y)
{
	return x+y;
}
//C++14中不再需要显式指定返回类型
auto func(int x, int y)
{
	return x+y;
}
```
## 4.内存申请与释放
- 零指针
  - NULL：当我们使用NULL表示空指针时，容易忽略它同时是一个int型常量。

  - nullptr：表示严格意义上的空指针
## 5.For循环
- 基于范围的for循环
  - 在循环头的圆括号中，由冒号":"分为两部分，第一部分是用于迭代的变量，第二部分则表示将被迭代的范围。如：
```c++
#include <iostream>
	using namespace std;
	int main() {
		int arr[3] = {1, 3, 9};
		for (int e : arr) // auto e:arr 也可以
			cout << e << endl;
		return 0;
	}
```
# session 2 认识对象
## 对象
- 对象=静态特征+动态特征
- 封装（类）={属性/数据，服务/函数}
- 封装实质是引入新的类型，被称为用户自定义类型
## 类 class
- 类= “属性/数据” + “服务/函数”
- class 用户自定义的类型
  - 包含函数与数据的特殊“结构体”，用于扩充C++语言的类型体系
  - 类中包含的函数，称为“成员函数”
  - 包含的数据，称为“成员变量”
- 成员函数必须在类内声明，但定义（实现）可以**在类内**或者**类外**。
### 写法
>通常，类的声明放在头文件中，而类的成员函数实现（也叫定义）则放在实现文件中。
>为了便于管理和代码复用，一般是将不同的类分别保存为不同的头文件和实现文件。
- 在头文件中声明类class
```c++
// matrix.h
#ifndef MATRIX_H
#define MATRIX_H

class Matrix {
	int data[6][6];
public:
	void fill(char dir);
};
#endif 
```
- 两种定义成员函数的方式
  - 在实现文件中定义成员函数
```c++
// matrix.cpp
#include "matrix.h"

void Matrix::fill(char dir) //类外需要类名限定
{
	... // 函数实现
}
```
- 在类内定义成员函数
```c++
class Matrix {
public:
	void fill(char dir) { 
		...;  
	}
};
//为了方便解决依赖关系，复杂的成员函数声明和定义一般是分离的，很少使用类内定义的方式。
```

### 类成员的访问
#### 访问权限
类的成员（数据、函数）可以根据需要分成组，不同组设置不同的访问权限
- public
被public修饰的成员可以在类外访问。
- private
默认权限
被private修饰的成员不允许在类外(非该类的成员函数)访问，class中成员的缺省属性为private。
- protected
以后介绍。
```c++
// matrix.cpp
#include "matrix.h"

void Matrix::add(Matrix a) {
    for(int i=0; i<6; i++){
        for(int j=0; j<6; j++) {
   data[i][j] += a.data[i][j]; // 可以在类内用“.”操作访问同一类下的私有成员
        }
    }
}
```
#### 访问方式
- 通过“对象名.成员名”的形式，可以使用对象的数据成员，或调用对象的成员函数。在类外使用时仅限于访问public权限的成员
- 同样，可以使用“对象指针->成员名”形式访问数据成员或成员函数。在类外也只限于访问public权限的成员。
## this指针
- 所有成员函数的参数中，隐含着一个指向当前对象的指针变量，其名称为this
## 内联函数nline 修饰
- 函数调用要进行一系列准备和后处理工作(压栈、跳转、退栈、返回等)，所以函数调用是一个比较慢的过程。
- 避免将内联函数的声明和定义分开：编译时内联实现，因此多文件编译时，要将实现写在头文件中，否则无效
- 定义在类声明中的函数，默认为内联函数
- 一般构造函数、析构函数都被定义为内联函数
- 编译器“有权”拒绝不合理的请求
```c++
//使用内联函数，编译器自动产生等价的表达式
inline int max(int a, int b) { 
    return a > b ? a : b; 
}
cout << max(a, b) << endl;
//上述代码等价于
cout << (a > b ? a : b) << endl;
```
### 内联函数和宏定义的区别
- 宏代码容易出错，编译预处理器在拷贝代码时，可能产生意想不到的边界效应。
```c++
#define MAX(a, b) (a) > (b) ? (a) : (b)

cout << MAX(a, b) + 2 << endl;
cout << (a) > (b) ? (a) : (b) + 2 << end; //编译预处理器结果失败
```
```c++
//上述代码更改如下可正常工作。
#define MAX(a, b) ((a) > (b) ? (a) : (b))

cout << MAX(a, b) + 2 << endl;
cout << ((a) > (b) ? (a) : (b)) + 2 << end; // 编译预处理器结果成功
```
- 显然不是万无一失的，例如下面的这种情况。

```c++
#define MAX(a, b) ((a) > (b) ? (a) : (b))

cout << MAX(a++, b) + 2 << endl;

cout << ((a++) > (b) ? (a++) : (b)) + 2 << end; // a被两次求值
```
- 因为宏代码是直接拷贝到指定位置的，很多缺陷不可避免。内联函数生成的是，和函数等价的表达式。
- 内联函数可以执行类型检查，进行编译期错误检查。
内联函数可调试，而宏定义的函数不可调试。在Debug版本，内联函数没有真正内联，而是和一般函数一样，因此在该阶段可以被调试。在Release版本，内联函数实现了真正的内联，增加执行效率。
- 宏定义的函数无法操作私有数据成员。
宏使用的最常见场景：字符串定义、字符串拼接、标志粘贴(教材第9章p221~222)

```c++
//test.h
class Test {
	int* data;
public:
	void setdata(const int* d) {data = d; } //内联函数
	const int* getdata() {return this->data;}//内联函数
	void operation1(int);
	Test(int i){ 
		if (i>0) 
			data = new int[i];
		else
			data = nullptr;
 	} //内联函数
	~Test(){delete[] data;} //内联函数
};
```
## 拓展：如何在C++中打印变量类型
```c++
#include<iostream>
#include<typeinfo>
#include<cxxabi.h>//C++ ABI库
class Test{

};
template<typename T>
char* get_type(const T& instance){//模板函数get_type接受任意类型的变量作为参数
return abi::__cxa_demangle(typeid((instance)).name(), nullptr, nullptr, nullptr);
//在函数内部，get_type使用typeid来获取传入变量的type_info对象
//用type_info对象上的name()方法获取变量的混淆类型名称
//函数将混淆类型名称传递给cxxabi.h库中的__cxa_demangle函数，该函数解开名称并返回一个指向解开名称的字符指针
}
int main(){
	auto* x = "abc";//指向字符串"abc"的指针
	auto y = new int[5];//指向整型数组的指针
	auto z = Test();//类Test
	std::cout << get_type(x) << std::endl;//char const*
	std::cout << get_type(y) << std::endl;//int*
	std::cout << get_type(z) << std::endl;//Test
}
```