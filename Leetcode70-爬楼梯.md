---
title: Leetcode70.爬楼梯
date: 2020-05-23 13:41:47
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode70.爬楼梯

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

[题目链接](https://leetcode-cn.com/problems/climbing-stairs)

<!--more-->

示例 1：

```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。

1. 1 阶 + 1 阶

2. 2 阶
```

示例 2：

```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。

1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```



#### 思路

动态规划，令`dp[i]`代表跳到第`i`阶楼梯的方法次数，可以很容易的得到：

`dp[i] = dp[i-1] + dp[i-2]`。初始化：`dp[1]=1, dp[2] = 2`。

注意：开辟数组空间时开辟`n+2`个空间，可以减少对`n=1`的特例判断。



#### 代码实现

```java
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 2];
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i < n + 1; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

