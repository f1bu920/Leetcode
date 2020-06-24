---
title: Leetcode198.打家劫舍
date: 2020-05-29 09:16:28
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode198.打家劫舍

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。

[题目链接](https://leetcode-cn.com/problems/house-robber)

<!--more-->

示例 1:

```
输入: [1,2,3,1]
输出: 4
解释: 偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
```



示例 2:

```
输入: [2,7,9,3,1]
输出: 12
解释: 偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。
```



#### 思路

算是我遇到过的最简单的动态规划了...

令`dp[i]`代表遍历到`nums[i]`的偷窃钱的最大值，又因为不能连续，所以可以很轻易的得到状态转移方程：
$$
dp[i] = Math.max(dp[i-2]+nums[i],dp[i-1])
$$
考虑初始化：`i-2`要大于等于0，所以`i=0`和`i=1`特殊讨论：`dp[0] = nums[0]`、`dp[1]=Math.max(nums[0],nums[1])`。



#### 代码实现

```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int len = nums.length;
        if (len == 1) {
            return nums[0];
        }
        int[] dp = new int[len];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        for (int i = 2; i < len; i++) {
            dp[i] = Math.max(dp[i - 2] + nums[i], dp[i - 1]);
        }
        return dp[len - 1];
    }
}
```

