---
title: leetcode_49
date: 2023-01-23 17:22:50
tags: leetcode
---
## leetcode_49 字母异位词分组
> 给你一个字符串数组，请你将字母异位词组合在一起。可以按任意顺序返回结果列表。
字母异位词，是由重新排列源单词的字母得到的一个新单词，所有源单词中的字母通常恰好只用一次。
输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
输出: [ ["bat" ] , [ "nat","tan" ] , [ "ate","eat","tea" ] ]
<!-- more -->
### 方法一 以排好序的string作为键值
```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> mp;
        for (string& str: strs) {
            string key = str;
            sort(key.begin(), key.end());
            mp[key].emplace_back(str);
        }
        vector<vector<string>> ans;
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            ans.emplace_back(it->second);
        }
        return ans;
    }
};
```
### 方法二 计数，以每个字母出现的次数作为键值
```c++
	class Solution {
	public:
		vector<vector<string>> groupAnagrams(vector<string>& strs) {
			auto arrayHash = [fn = hash<int>{}](const array<int, 26>& arr)->size_t {
                //size_t 类型表示C中任何对象所能达到的最大长度，它是无符号整数
                /*
                * accumulate()中的第四个参数项要传入一个二元操作(BinaryOperation)规则，告诉它如何将当前元素与累积量做操作
                * 它隐式地调用(size_t)acc和(int)num这两个量，默认情况下做简单的相加运算。
                */
				return accumulate(arr.begin(), arr.end(), (size_t)0, [&](size_t acc, int num) {
                    return (acc << 1) ^ fn(num); // hash运算结果移位相加
                    });
			};
            /*
            * 由于key的类型是array<int, 26>，属于用户自定义的一个数据类型，编译器无法针对用户自定义的数据类型做两个元素是否相等的判断
            * 所以，要告诉unordered_map你是如何确定key与key之间是否冲突(或者是否相等)的。
            * 正因如此，unordered_map的API中的第三个参数项就会让用户传入一个运算规则的函数的类型
            * 而前面写的arrayHash这个类(class)实际上是一个lambda expression(你也可以把它看作是一个仿函数(functor)的类)
            * 要获取一个显式的类的类型是容易的，但这里是隐式的，就要借助于decltype获得arrayHash的type了
            * (补充一点，lambda表达式很多都是通过decltype()的技巧获取其类型的，这也是C++11的重大进步之一)
            */
			unordered_map<array<int, 26>, vector<string>, decltype(arrayHash)> mp(0, arrayHash);
			for (string& str : strs) {
				array<int, 26> counts{};
				int length = (int)str.length();
				for (int i = 0; i < length; ++i) counts[(size_t)str[i] - 'a'] ++;
                /*
                * mp[counts]过程就会调用arrayHash计算counts的hash值
                * 在哈希表中寻找对应哈希值的篮子(busket)，并将该counts对应的str挂在对应篮子的链表尾部
                * (对于不存在的哈希值，对应的篮子是一个空链表，将str挂篮子的链表尾部这一操作仍然不变，
                * 如此一来就统一了emplace_back()的操作：只负责在篮子的链表的尾部添加string)
                */
				mp[counts].emplace_back(str);
			}
			vector<vector<string>> ans;
			for (auto it = mp.begin(); it != mp.end(); ++it) ans.emplace_back(it->second);
			return ans;
		}
	};
```
### 方法二优化 把频次表转换为string
```c++
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    vector<vector<string>> res ;
    map<string, vector<string>> map ;

    // 统计string的各字母频次,以频次为key直接加入队列
    for (auto s : strs) {
        string sts = string(26, '0') ;
        for (auto c : s)  ++ sts[c-'a'] ;
        map[sts].emplace_back (s) ;
    }
    for (auto e : map)  res.emplace_back(e.second) ;

    return res ;
}
```