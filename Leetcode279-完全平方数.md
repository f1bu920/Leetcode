---
title: Leetcode279.完全平方数
date: 2020-08-04 08:47:38
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode279.完全平方数

给定正整数 `n`，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 `n`。你需要让组成和的完全平方数的个数最少。

[题目连接](https://leetcode-cn.com/problems/perfect-squares)

<!--more-->

示例 1:

```
输入: n = 12
输出: 3 
解释: 12 = 4 + 4 + 4.
```



示例 2:

```
输入: n = 13
输出: 2
解释: 13 = 4 + 9.
```



### 思路

令`dp[i]`代表组成`i`的完全平方数的最少个数，可得状态转移方程为`dp[i] = min(dp[i],dp[i-k]+1)`，`k`属于完全平方数。



### 代码实现

```java
class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        //初始化设值
        dp[0] = 0;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; i - j * j >= 0; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }
        return dp[n];
    }
}
```

上面代码中重复计算了多次`j`的平方，可以提前创建一个数组存储完全平方数。