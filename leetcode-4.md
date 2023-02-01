---
title: leetcode-4
date: 2023-01-14 21:34:13
tags: leetcode
---
>4. 寻找两个正序数组的中位数
给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。
算法的时间复杂度应该为 O(log (m+n))
<!-- more -->

思路：
- 看到时间复杂度自然想到应该使用二分查找法。  
- 中位数的定义：如果有序数组长度是奇数，中位数就是最中间的数字，如果是偶数，是最中间两个数字的平均值。
- 这里对于两个有序数组也是一样的：假设两个有序数组的长度分别为m和n，由于两个数组长度之和 m+n 的奇偶不确定，因此需要分情况来讨论。
- 简化代码（不分情况讨论）：对第(m+n+1) / 2 和 (m+n+2) / 2 个求其平均值即可（奇偶数均适用）。假如m+n为奇数，则两值相等。

- 如何实现找到第K个元素。
- 首先，为了避免产生新的数组导致时间复杂度增加，使用变量i和j标记数组nums1和nums2的起始位置。
- 边界处理
- 使用二分法在两个有序数组中找到第K个元素：对K二分，即分别在nums1和nums2中查找第K/2个元素，**注意：由于两个数组的长度不定，所以可能某个数组没有第K/2个数字**
- 先检查数组中是否存在第K/2个数字，
  - 如果存在取出来
  - 否则赋值上一个整型最大值。
- 如果某个数组没有第K/2个数字，那么我们就淘汰另一个数字的前K/2个数字即可。有没有可能两个数组都不存在第K/2个数字呢，这道题里是不可能的，因为我们的K不是任意给的，而是给的m+n的中间值，所以必定至少会有一个数组是存在第K/2个数字的。
- 最后就是二分法的核心：比较这两个数组的第K/2小的数字midVal1和midVal2的大小，如果第一个数组的第K/2个数字小的话，那么说明我们要找的数字肯定不在nums1中的前K/2个数字，所以我们可以将其淘汰，将nums1的起始位置向后移动K/2个，并且此时的K也减去K/2，调用递归。反之，我们淘汰nums2中的前K/2个数字，并将nums2的起始位置向后移动K/2个，并且此时的K也自减去K/2，调用递归即可
```c++
class Solution {
  public double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.length();
        int n = nums2.length();
        int left = (m + n + 1) / 2;
        int right = (m + n + 2) / 2;
        return (findKth(nums1, 0, nums2, 0, left) + findKth(nums1, 0, nums2, 0, right)) / 2.0;
    }
    //i: nums1的起始位置 j: nums2的起始位置
    public int findKth(vector<int>& nums1, vector<int>& nums2, int j, int k){
        if( i >= nums1.length()) return nums2[j + k - 1];//nums1为空数组
        if( j >= nums2.length()) return nums1[i + k - 1];//nums2为空数组
        if(k == 1){
            return Math.min(nums1[i], nums2[j]);
        }
        int midVal1 = (i + k / 2 - 1 < nums1.length) ? nums1[i + k / 2 - 1] : Integer.MAX_VALUE;
        int midVal2 = (j + k / 2 - 1 < nums2.length) ? nums2[j + k / 2 - 1] : Integer.MAX_VALUE;
        if(midVal1 < midVal2){
            return findKth(nums1, i + k / 2, nums2, j , k - k / 2);
        }else{
            return findKth(nums1, i, nums2, j + k / 2 , k - k / 2);
        }        
    }
}
```
