---
title: Leetcode120.三角形最小路径和
date: 2020-07-14 11:14:04
categories: Leetcode
tags:
  - 动态规划
---

##  Leetcode120.三角形最小路径和

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。

 [题目链接](https://leetcode-cn.com/problems/triangle)

<!--more-->

例如，给定三角形：

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。
```

说明：

如果你可以只使用 O(n) 的额外空间（n 为三角形的总行数）来解决这个问题，那么你的算法会很加分。



### 思路

令`dp[i][j]`表示到达`(i,j)`位置的最小路径和，所以可得状态转移方程为$dp[i][j] = Math.min(dp[i-1][j-1],dp[i-1][j])+nums[i][j]$.

考虑初始化：对于三角形的最左边和最右边，分别有`dp[i][0] = dp[i-1][0] + nums[i][0]`和`dp[i][i]= dp[i-1][i-1] + nums[i][i]`.

最后的结果就是最后一行中的最小值。



### 代码实现

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if (triangle == null || triangle.size() == 0) {
            return 0;
        }
        int minTotal = Integer.MAX_VALUE;
        int m = triangle.size();
        int n = triangle.get(m - 1).size();
        int[][] dp = new int[m][n];
        dp[0][0] = triangle.get(0).get(0);
        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0] + triangle.get(i).get(0);
            dp[i][i] = dp[i - 1][i - 1] + triangle.get(i).get(i);
        }
        for (int i = 2; i < m; i++) {
            for (int j = 1; j < i; j++) {
                dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j]) + triangle.get(i).get(j);
            }
        }
        for (int i = 0; i < n; i++) {
            minTotal = Math.min(minTotal, dp[m - 1][i]);
        }
        return minTotal;
    }
}
```



