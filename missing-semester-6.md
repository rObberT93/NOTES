---
title: missing_semester_6
date: 2023-01-28 19:28:03
tags: missing semester
---
## 版本控制系统 (VCSs) 
- 用于追踪源代码（或其他文件、文件夹）改动的工具
- 方便协作编码
<!-- more -->
- 易于知道以下问题：
  - 当前模块是谁编写的？
  - 这个文件的这一行是什么时候被编辑的？是谁作出的修改？修改原因是什么呢？
  - 最近的1000个版本中，何时/为什么导致了单元测试失败？
# git数据模型
## 快照
- 文件：Blob对象（数据对象），也就是一组数据。
- 目录：“树”，它将名字与 Blob 对象或树对象进行映射（使得目录中可以包含其他目录）。
- 快照：被追踪的最顶层的树
```
<root> (tree)
|
+- foo (tree)
|  |
|  + bar.txt (blob, contents = "hello world")
|
+- baz.txt (blob, contents = "git is wonderful")
```
### 历史记录建模：关联快照
- 在 Git 中，历史记录是一个由快照组成的有向无环图
- 每个快照都有一系列的“父辈”，也就是其之前的一系列快照。注意，快照具有多个“父辈”而非一个，因为某个快照可能由多个父辈而来
- 每个快照都有一系列的“父辈”，也就是其之前的一系列快照。注意，快照具有多个“父辈”而非一个，因为某个快照可能由多个父辈而来
```
o <-- o <-- o <-- o
            ^  
             \
              --- o <-- o
//o 表示一次提交（快照）
//箭头指向了当前提交的父辈
```
## Git 的数据模型
```
// 文件就是一组数据
type blob = array<byte>

// 一个包含文件和目录的目录
type tree = map<string, tree | blob>

// 每个提交都包含一个父辈，元数据和顶层树
type commit = struct {
    parent: array<commit>
    author: string
    message: string
    snapshot: tree
}
```
### 对象和内存寻址
- Git 中的对象可以是 blob、树或提交：
```
type object = blob | tree | commit
```
- Git 在储存数据时，所有的对象都会基于它们的 SHA-1 哈希 进行寻址
```
objects = map<string, object>

def store(object):
    id = sha1(object)
    objects[id] = object

def load(id):
    return objects[id]
```
#### SHA-1 
SHA-1 (Secure Hash Algorithm 1) 是一种密码散列函数，用于对数据进行哈希运算。它可以将任意长度的输入数据转换为固定长度的输出值，即哈希值。  

SHA-1哈希值的长度为160位，输出的哈希值是一个十六进制的字符串。  

SHA-1算法比较常用在版本控制系统(如Git)中用于确定文件或目录的唯一性，因为SHA-1的哈希值可以唯一的表示一个文件或目录的版本。并且，SHA-1还被用于确定文件完整性和认证。  

由于SHA-1算法可能被破解，因此已经被更安全的算法（如SHA-256和SHA-3）所取代。
``git hash-object 文件名``查看文件散列值
``git cat-file -p 哈希值``通过哈希值查看 某文件 的内容
### 引用
- 引用是指向提交的指针。
- 与对象不同的是，引用是可变的（引用可以被更新，指向新的提交）
```
references = map<string, string>

def update_reference(name, id):
    references[name] = id

def read_reference(name):
    return references[name]

def load_reference(name_or_id):
    if name_or_id in references:
        return load(references[name_or_id])
    else:
        return load(name_or_id)
```
### 仓库=对象+引用
## 暂存区
## Git 的命令行接口
- 基础
  - ``git help <command>``: 获取 git 命令的帮助信息
  - ``git init``: 创建一个新的 git 仓库，其数据会存放在一个名为 .git 的目录下
  - ``git status``: 显示当前的仓库状态
  - ``git add <filename>``: 添加文件到暂存区
  - ``git commit``: 创建一个新的提交
  - ``git log``: 显示历史日志
  - ``git log --all --graph --decorate``: 可视化历史记录（有向无环图）
  - ``git diff <filename>``: 显示与暂存区文件的差异
  - ``git diff <revision> <filename>``: 显示某个文件两个版本之间的差异
  - ``git checkout <revision>``: 更新 HEAD 和目前的分支
- 分支和合并
  - ``git branch``: 显示分支
  - ``git branch <name>``: 创建分支
  - ``git checkout -b <name>``: 创建分支并切换到该分支
    - 相当于 ``git branch <name>; git checkout <name>``
  - ``git merge <revision>``: 合并到当前分支
  - ``git mergetool``: 使用工具来处理合并冲突
  - ``git rebase``: 将一系列补丁变基（rebase）为新的基线
- 远端操作
  - ``git remote``: 列出远端
  - ``git remote add <name> <url>``: 添加一个远端
  - ``git push <remote> <local branch>:<remote branch>``: 将对象传送至远端并更新远端引用
  - ``git branch --set-upstream-to=<remote>/<remote branch>``: 创建本地和远端分支的关联关系
  - ``git fetch``: 从远端获取对象/索引
  - ``git pull``: 相当于 git fetch; git merge
  - ``git clone``: 从远端下载仓库
- 撤销
  - ``git commit --amend``: 编辑提交的内容或信息
  - ``git reset HEAD <file>``: 恢复暂存的文件
  - ``git checkout -- <file>``: 丢弃修改
-`` git restore``: git2.32版本后取代git reset 进行许多撤销操作
- Git 高级操作
  - ``git config``: Git 是一个 高度可定制的 工具
  - ``git clone --depth=1``: 浅克隆（shallow clone），不包括完整的版本历史信息
  - ``git add -p``: 交互式暂存
  - ``git rebase -i``: 交互式变基
  - ``git blame``: 查看最后修改某行的人
  - ``git stash``: 暂时移除工作目录下的修改内容
  - ``git bisect``: 通过二分查找搜索历史记录
  - ``.gitignore``: 指定 故意不追踪的文件