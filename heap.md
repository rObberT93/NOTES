---
title: heap
date: 2023-02-04 15:16:29
tags: dsa
---
## directory
- 堆的基本存储
- shift up 操作
- shift down 操作
- 堆排序
- 优化堆排序
- 索引堆
<!-- more -->
## 堆的基本存储
完全二叉树，用数组存储。
父节点值大于两个子节点，左孩子值不小于右孩子。
父节点下标i，左孩子下标2i，右孩子下标2i+1。
## shiftup操作
比较子节点和父节点

## shiftdown操作
从最大堆中取出一个元素（根节点），填补这个最大堆。
- 把数组最后以为放到根节点
- 把根节点一步步往下挪
  - 如果比两个孩子都笑，先比较两个孩子哪个大，和大的交换位置。
- 交换至比两个孩子都大，操作完成。
```cpp
private void shiftDown(int k){
    while( 2*k <= count ){
        int j = 2*k; // 在此轮循环中,data[k]和data[j]交换位置
        if( j+1 <= count && data[j+1]>data[j])
            j ++;
            // data[j] 是 data[2*k]和data[2*k+1]中的最大值
        if( data[k]>data[j]) break;
        swap(data[k],data[j]);
        k = j;
    }
}
```
## 堆排序
- 从第一个非叶子节点（最下右）开始逐一向前分别把每个元素作为根节点进行shift down操作，维护最大堆。
## 优化堆排序
原地堆排序
- 对于一个最大堆，首先交换index 0(max, 记为元素v) 和n-1(记为元素w)
- 使得最大元素在数组末尾(v)
- 对W元素进行 shift down 操作，重新生成最大堆
- 交换新生成的最大数和整个数组倒数第二位置，此时倒数第二位置就是第二大数据，这个过程以此类推。
## 索引堆
使用int类型数组，用于存放索引信息
- 优化交换元素的消耗，操作的是索引
- 加入的数据位置固定，方便寻找