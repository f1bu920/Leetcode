---
title: Leetcode152.乘积最大子数组
date: 2020-05-18 09:15:41
categories: Leetcode
tags:
  - 动态规划
  - Array
---

## Leetcode152.乘积最大子数组

给你一个整数数组 `nums` ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

 [题目链接](https://leetcode-cn.com/problems/maximum-product-subarray)

<!--more-->

示例 1:

输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
示例 2:

输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。

#### 思路

因为是乘积，一个正数乘以负数就变成了负数，所以最大值和最小值是可以相互转换的。

令`dp[i][j]`表示以`nums[i]`结尾的连续子数组的最值，其中`j=0`代表最小值，`j=1`代表最大值。

- 当`nums[i]>=0`时，最大值乘以正数仍然是最大值，最小值乘以负数仍然是最小值。
- 当`nums[i]<0`时，最大值乘以负数就变成了最小值，最小值乘以负数就变成了最大值。
- 如果`nums[i]>0`时，之前的最大值小于0，`dp[i-1][1]<0`，那么取两者的最大值。
- 其他情况同理。

所以可得状态转移方程为：
$$
dp[i][1]=max(nums[i-1][1]*nums[i],nums[i]),nums[i]>=0;\\
dp[i][0]=min(nums[i-1][0]*nums[i],nums[i]),nums[i]>=0;\\
dp[i][1]=max(nums[i-1][0]*nums[i],nums[i]),nums[i]<0;\\
dp[i][0]=min(nums[i-1][1]*nums[i],nums[i]),nums[i]<0;
$$
最后遍历`dp[i][1]`，找到最大值。



#### 代码实现

```java
class Solution {
    public int maxProduct(int[] nums) {
        int len = nums.length;
        if (len == 0) {
            return 0;
        }
        int[][] dp = new int[len][2];
        dp[0][0] = nums[0];
        dp[0][1] = nums[0];
        for (int i = 1; i < len; i++) {
            if (nums[i] >= 0) {
                dp[i][1] = Math.max(dp[i - 1][1] * nums[i], nums[i]);
                dp[i][0] = Math.min(dp[i - 1][0] * nums[i], nums[i]);
            } else {
                dp[i][1] = Math.max(dp[i - 1][0] * nums[i], nums[i]);
                dp[i][0] = Math.min(dp[i - 1][1] * nums[i], nums[i]);
            }
        }
        int result = dp[0][1];
        for (int i = 1; i < len; i++) {
            result = Math.max(result, dp[i][1]);
        }
        return result;
    }
}
```

