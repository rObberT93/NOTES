---
title: set
date: 2023-01-11 12:20:26
tags: 数据结构
---
# set
- set是一个集合（内部元素有且只有一份），且元素有序排列——set适合用来去重和排序
- 使用 set 容器存储的各个键值对，要求键 key 和值 value 必须相等【map存储的键值对，ke不是必须相等】
```
{<'a', 1>, <'b', 2>, <'c', 3>}//各键值对的键和值不相等
{<'a', 'a'>, <'b', 'b'>, <'c', 'c'>}//各键值对的键和值对应相等
```
<!-- more -->
- 复杂度——O(logn)
- 红黑树——平衡二叉树
- 不能修改set中的值，修改-->删除当前值，插入新值
- 头文件`#include<set>`
- 默认构造函数：`set<int>s;` `set<string >s;`
- 创建同时初始化`set<int>s{1,2,3}` `set<string>s{"string_a","string_b"};`
- 复制构造函数：`set<int>copyset(s)`
- 移动构造函数

|成员函数|用法|
| :--- | :--- |
|s.begin()|返回指向容器中(已排好序的第一个)第一个元素的双向迭代器
|s.end()|返回指向容器(已排好序的)最后元素所在位置**后一个位置**的双向迭代器
|s.rbegin()|返回指(已排好序的)向最后一个元素的反向双向迭代器
|s.rend()|返回指向(已排好序的)第一个元素所在位置前一个位置的反向双向迭代器
|s.insert(x)|插入元素x
|s.erase(x)|清除元素x
|s.size()|set的大小
|s.find(x)|查找值为x的元素，找到则返回指向x的双向迭代器；未找到则返回和 end() 方法一样的迭代器
|s.lower_bound(val)|返回指向第一个大于或等于 val 的元素的双向迭代器
|s.count()|统计set中x的数量，出现为1，不出现为0
|s.upper_bound(val)|返回指向第一个大于 val 的元素的迭代器
|s.empty()|空返回 true；非空 false
|s.swap()|交换 2 个 set 容器中存储的所有元素
|s.clear()|清空 set 容器中所有的元素
|s.emplace()|在当前 set 容器中的指定位置直接构造新元素(效果和 insert() 一样，但效率更高)
```c++
#include<iostream>
#include<set>
using namespace std;

int main()
{
    set<int>s;
    s.insert(9);s.insert(5);s.insert(9);s.inset(1);
    cout<<s.size()<<endl;//3
    s.erase(5);
    auto it=s.find(5);
    if(it==s.end()) cout<<"can not find"<<endl;//can not find
    for(auto it=s.begin();it!=s.end();it++)
        cout<< *it<<" ";//1 9
    cout<<endl;
}
```