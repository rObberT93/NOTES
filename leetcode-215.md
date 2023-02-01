---
title: leetcode-215
date: 2023-01-27 14:43:38
tags: leetcode
---
# 215. 数组中的第K个最大元素
> 给定整数数组 nums 和整数 k，请返回数组中第 k 个最大的元素。
请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。
你必须设计并实现时间复杂度为 O(n) 的算法解决此问题。

<!-- more -->
- 很疑惑的一个排序题，要求big O(n)的算法解决。
- 本质是一个快排收缩边界的想法，将数组分成两部分：大于或等于枢轴元素的元素，和小于枢轴元素的元素。
- 大小在以1/2的速度收缩，所以是属于O(n)的算法。
- 为了避免the worst case，选择随机主元下标
- 建议在调用find函数之前，先将数组打乱，这样可以防止在已经排序的数组上运行的速度很慢.
```c++
class Solution {
public:
    void find(int begin,int end,vector<int>& nums,int k)
    {
        // base case for recursion: stop when partition is complete
        if(end-begin<1) return;
        int pivot = begin + (rand() % (end - begin + 1)); // get a random pivot
        swap(nums[begin], nums[pivot]);
        int base=nums[begin];
        int index=begin;
        for(int i=begin+1;i<=end;i++)
        {
            if(nums[i]>=base)
            {
                swap(nums[index+1],nums[i]);
                index++;
            }
        }
        swap(nums[begin],nums[index]);
        if(index<k)find(index+1,end,nums,k);
        else if(index>k)find(begin,index-1,nums,k);
        else return;
    }
    int findKthLargest(vector<int>& nums, int k) {
        int n=nums.size();
        random_shuffle(nums.begin(), nums.end());// 提高效率
        find(0,n-1,nums,k-1);
        return nums[k-1];
    }
};
```
use a while loop instead of recursion, which is more readable and avoid the risk of stack overflow
```c++
class Solution {
public:
    int partition(vector<int>& nums, int left, int right) {
        int pivot = nums[left];
        int i = left, j = right;
        while (i < j) {
            while (i < j && nums[j] <= pivot) j--;
            if (i < j) nums[i++] = nums[j];
            while (i < j && nums[i] >= pivot) i++;
            if (i < j) nums[j--] = nums[i];
        }
        nums[i] = pivot;
        return i;
    }

    int findKthLargest(vector<int>& nums, int k) {
        int left = 0, right = nums.size() - 1;
        while (true) {
            int pos = partition(nums, left, right);
            if (pos == k - 1) return nums[pos];
            else if (pos < k - 1) left = pos + 1;
            else right = pos - 1;
        }
    }
};
```