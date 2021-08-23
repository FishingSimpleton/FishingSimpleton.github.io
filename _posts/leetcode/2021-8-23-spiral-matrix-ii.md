---
layout: blog
book: true
title:  "leetcode[59. 螺旋矩阵 II] by DylanChou 刷leetcode心得"
background-image: http://ot1cc1u9t.bkt.clouddn.com/17-7-15/82431810.jpg
date:   2021-8-23 10:24:25
category: LeetCode
tags:
- LeetCode
- 矩阵
- vector
---

#### [59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

难度中等466收藏分享切换为英文接收动态反馈

给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```

**示例 2：**

```
输入：n = 1
输出：[[1]]
```

 

**提示：**

- `1 <= n <= 20`

通过次数118,787

提交次数149,694

##### 思路:

按层逐步生成

层数为n/2，n为奇数最后添加最中心元素。



```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>>result(n,vector<int>(n));
        int count = 1;
        for (int i = 0; i < n / 2; i++)
        {
            for (int j = i; j < n - i; j++)
            {
                result[i][j] = count++;
            }
            for (int j = i + 1; j < n - i - 1; j++)
            {
                result[j][n - i - 1] = count++;
            }
            for (int j = n - i - 1; j >= i; j--)
            {
                result[n - i - 1][j] = count++;
            }
            for (int j = n - i - 2; j > i; j--)
            {
                result[j][i] = count++;
            }
            cout << count;
        }
        if (n % 2)
            result[n / 2][n / 2] = count;

        return result;
    }
    
};
```

