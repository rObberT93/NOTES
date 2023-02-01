---
title: QT
date: 2023-01-22 14:03:59
tags: QT
---
# QT basic
## 1.前言
1.1 跨平台图形界面引擎
1.2 优点
- 1.2.1 跨平台
- 1.2.2 接口简单
- 1.2.3 优化内存回收
<!-- more -->
## 2. 创建工程
### 2.1 类
- QWidget(父类) 最简单的窗口
- QMainWindow(子类) 派生类 多菜单栏 工具栏 状态栏
- QDialog(子类)对话框
### 2.2 版本控制
- svn solve commit lock
- vss
- git
### 2.3 生成文件
- .pro 工程文件
- .h
- .cpp
### 2.4 main函数
- QApplication a 应用程序对象有且仅有一个
- myWidget w 实例化窗口对象
- w.show() 调用show方法显示窗口
- return a.exec() 让应用程序进入消息循环（捕捉用户操作 让界面不会一闪而过），让代码阻塞到这行
### 2.5 .pro文件解读
```c++
QT       += core gui

greaterThan(QT_MAJOR_VERSION, 4): QT += widgets//大于4版本以上 包含widget模块

TARGET = 01FirstProject//目标：生成的.exe程序名称 换名称可以直接改这里
TEMPLATE = app//模板 应用程序模板 applictaion
//lib
//vcapp
DEFINES += QT_DEPRECATED_WARNINGS


SOURCES += \    //源文件
        main.cpp \
        mywidget.cpp

HEADERS += \    
        mywidget.h//头文件

FORMS += \
        mywidget.ui
```
### 2.6 命名规范
- 类名 首字母大写，单词和单词之间首字母大写
- 函数名 变量名称 首字母小写，单词和单词之间首字母大写

### 2.7 快捷键
注释 ctrl + /  
运行 ctrl + r  
编译 ctrl + b  
字体缩放 ctrl+ 鼠标滚轮  
查找 ctrl + f  
整行移动 ctrl + shift + ↑ 或者 ↓  
帮助文档 F1  
自动对齐 ctrl + i  
同名之间的.h 和.cpp切换 F4  

### 2.8 帮助文档 
第一种 F1
第二种 帮助文档界面  
第三种 C:\Qt\Qt5.9.0\5.9\mingw53_32\bin assistant
## 3. 按钮控件
- 3.1 创建    QPushButton *btn=new - QPushButton;
- 3.2 设置父亲 btn->setParent(this);
- 3.3 设置文本  btn->setText("第一个按钮");
  - 中文乱码问题：工具-选项-文本编辑器-行为-文件编码-默认编码UTF-8
- 3.4 设置位置 btn2->move(100,100);
- 3.5 重新指定窗口大小 resize(600,400);
- 3.6 设置窗口标题 setFixedSize(600,400);
- 3.7 设置窗口固定大小setFixedSize(600,400);
## 4.对象树
4.1 当创建的对象在堆区时，如果指定的父亲时QObject派生下来的类或者QObject的子类派生下来的类，可以不用管理释放的操作，对象会被放入对象树中。
4.2 一定程度上简化了内存回收的操作
## 5.窗口坐标系
(0,0)$\rightarrow$x
$\downarrow$y
5.1 左上角是(0,0)
5.2 以右为x的正方向
5.3 向下为y的正方向
## 6. 信号和槽
6.1 链接方式:connect
6.2 参数 
- 参数1：信号的发送者
- 参数2：发送的信号（函数的地址）
- 参数3：信号的接收者（窗口）
- 参数4：处理的槽函数（函数的地址）
6.3 松散耦合
6.4 实现点击按钮关闭窗口
6.5 connect(btn,&QPushButton::click,this,&QWidget::close)
## 7. 自定义的信号和槽
7.1 自定义信号
- 返回void
- 需要声明，不需要实现
- 可以有参数
7.2 自定义槽
- 返回void
- 需要声明，也需要实现
- 可以有参数，可以重载
- 写道public slot下，或者public或者全局函数下
7.3 触发自定义的信号 emit
7.4 实现下课后老师触发信号，学生响应信号的例子
## 8. 当自定义的信号和槽出现重载
8.1 需要利用函数指针明确指出指向函数的地址
8.2 void(Teacher:: * tSignal)(QString)=&Teacher::hungry;
8.3 QString转成char *
- .toUtf8();转为QByteArray
- .data();转为char *
### 拓展
1.信号可以连接信号
2.一个信号可以连接多个槽函数
3.多个信号可以连接同一个槽函数
4.信号和槽函数的参数必须类型一一匹配
5.信号和槽的参数个数可以不一致，信号的参数的个数可以多余槽函数的参数个数
6.利用QT4信号槽 连接无参版本
```cpp
connect(信号的发送者,SIGNAL(信号()),信号的解说这,SLOT(槽()));
```
优点：直观
缺点：编译器不检测参数类型
QT5版本以上
7.断开连接 disconnect
## lambda表达式
# QMainWindows