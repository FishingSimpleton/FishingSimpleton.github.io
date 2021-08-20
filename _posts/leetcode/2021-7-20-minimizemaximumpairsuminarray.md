<<<<<<< HEAD
---
layout: blog
book: true
title:  "leetcode[数组中最大数对和的最小值](双指针)by DylanChou 刷leetcode心得"
tags:

- LeetCode

- 双指针

- 排序
---
background-image: http://ot1cc1u9t.bkt.clouddn.com/17-7-15/82431810.jpg
date:   2021-7-20 10:22:10
category: LeetCode





#### [1877. 数组中最大数对和的最小值](https://leetcode-cn.com/problems/minimize-maximum-pair-sum-in-array/)

难度中等28收藏分享切换为英文接收动态反馈

一个数对 `(a,b)` 的 **数对和** 等于 `a + b` 。**最大数对和** 是一个数对数组中最大的 **数对和** 。

- 比方说，如果我们有数对 `(1,5)` ，`(2,3)` 和 `(4,4)`，**最大数对和** 为 `max(1+5, 2+3, 4+4) = max(6, 5, 8) = 8` 。

给你一个长度为 **偶数** `n` 的数组 `nums` ，请你将 `nums` 中的元素分成 `n / 2` 个数对，使得：

- `nums` 中每个元素 **恰好** 在 **一个** 数对中，且
- **最大数对和** 的值 **最小** 。

请你在最优数对划分的方案下，返回最小的 **最大数对和** 。

 

**示例 1：**

```
输入：nums = [3,5,2,3]
输出：7
解释：数组中的元素可以分为数对 (3,3) 和 (5,2) 。
最大数对和为 max(3+3, 5+2) = max(6, 7) = 7 。
```

**示例 2：**

```
输入：nums = [3,5,4,2,4,6]
输出：8
解释：数组中的元素可以分为数对 (3,5)，(4,4) 和 (6,2) 。
最大数对和为 max(3+5, 4+4, 6+2) = max(8, 8, 8) = 8 。
```

 

**提示：**

- `n == nums.length`
- `2 <= n <= 105`
- `n` 是 **偶数** 。
- `1 <= nums[i] <= 105`

通过次数11,714

提交次数13,941

##### 解法一：排序求和

```c++
class Solution {
public:
    int minPairSum(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int maxValue=0;
        for(int i=0;i!=nums.size()/2;i++)
        {
            maxValue=max(maxValue,(nums[i]+nums[(nums.size()-i-1)]));
        }
        return maxValue;

    }
};
```

##### 解法二：双指针W

```c++
class Solution {
public:
    int minPairSum(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int maxValue=0;
        int firNum=0,lastNum=nums.size()-1;
        while(firNum<lastNum)
        {
            maxValue=max(maxValue,(nums[firNum]+nums[lastNum]));
            firNum++;
            lastNum--;
        }
        
        return maxValue;

    }
};
```

