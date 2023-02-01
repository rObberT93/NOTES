---
title: leetcode_18
date: 2023-01-16 13:53:16
tags: leetcode
---
## leetcode_18 四数之和
重点：
- 双指针
- 去重及顺序
- 返回二维数组
- 整型溢出
<!-- more -->
>给你一个由 n 个整数组成的数组 nums ，和一个目标值 target，
请你找出并返回满足下述全部条件且不重复的四元组 [nums[a], nums[b], nums[c], nums[d]] （若两个四元组元素一一对应，则认为两个四元组重复）：
· 0 <= a, b, c, d < n
· a、b、c 和 d 互不相同
· nums[a] + nums[b] + nums[c] + nums[d] == target
可以按任意顺序返回答案

```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>>result;
        int n=nums.size();
        if(n<4) return result;
        sort(nums.begin(),nums.end());
        if((long)nums[0]+nums[1]+nums[2]+nums[3]>target) return result;
        for(int fir=0;fir<n-3;fir++)
        {
            //去重
            if(fir>0 && nums[fir]==nums[fir-1]) continue;
            for(int sec=fir+1;sec<n-2;sec++)
            {
                //去重
                if(sec>fir+1 && nums[sec]==nums[sec-1]) continue;
                int th=sec+1;
                int fo=n-1;
                while(th<fo)
                {
                    if((long)nums[th]+nums[fo]<(long)target-nums[fir]-nums[sec])
                        th++;
                    else if((long)nums[th]+nums[fo]>(long)target-nums[fir]-nums[sec])
                        fo--;
                    else
                    {
                        result.push_back({nums[fir],nums[sec],nums[th],nums[fo]});
                        //去重
                        while(th<fo && nums[fo-1]==nums[fo]) fo--;
                        //去重
                        while(th<fo && nums[th]==nums[th+1]) th++;
                        th++;
                        fo--;
                    }     
                }
            }
        }
        return result;
    }
};
//测试用例[1000000000,1000000000,1000000000,1000000000] -294967296
```
- 时间复杂度：$O(n^3)$，其中 $n$ 是数组的长度。排序的时间复杂度是 $O(n \log n)$，枚举四元组的时间复杂度是 $O(n^3)$，因此总时间复杂度为 $O(n^3+n\log n)=O(n^3)$
- 空间复杂度：$O(\log n)$，其中 $n$ 是数组的长度。空间复杂度主要取决于排序额外使用的空间。此外排序修改了输入数组 $nums$，实际情况中不一定允许，因此也可以看成使用了一个额外的数组存储了数组 $nums$ 的副本并排序，空间复杂度为 $O(n)$