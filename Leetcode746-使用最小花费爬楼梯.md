---
title: Leetcode746.使用最小花费爬楼梯
date: 2020-06-11 08:30:01
categories: Leetcode
tags:
  - 动态规划
---

##  Leetcode746.使用最小花费爬楼梯

给你一个整数数组 `cost` ，其中` cost[i]` 是从楼梯第 i 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。

你可以选择从下标为 0 或下标为 1 的台阶开始爬楼梯。

请你计算并返回达到楼梯顶部的最低花费。

#### [使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/)

<!--more-->

#### 思路

动态规划，有`n`个台阶，对应`0`到`n-1`，楼顶对应编号`n`，即计算到达下标`n`的最小花费。

创建长度为`n+1`的`dp`数组，其中可选择`0`或`1`为起始台阶，因此`dp[0] = dp[1] = 0`，每次可跳`0`或`1`阶，则动态转移方程为`dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])`。



#### 代码实现

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int[] dp = new int[n + 1];
        dp[0] = dp[1] = 0;
        for (int i = 2; i <= n; i++) {
            dp[i] = Math.min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
        }
        return dp[n];
    }
}
```

