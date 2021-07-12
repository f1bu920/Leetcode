---
title: Leetcode377.组合总和IV
date: 2021-04-24 10:21:18
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode377.组合总和IV

给你一个由 不同 整数组成的数组 nums ，和一个目标整数 target 。请你从 nums 中找出并返回总和为 target 的元素组合的个数。

题目数据保证答案符合 32 位整数范围。

 [题目链接](https://leetcode-cn.com/problems/combination-sum-iv)

<!--more-->

示例 1：

输入：nums = [1,2,3], target = 4
输出：7
解释：
所有可能的组合为：
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
请注意，顺序不同的序列被视作不同的组合。
示例 2：

输入：nums = [9], target = 3
输出：0


提示：

- 1 <= nums.length <= 200
- 1 <= nums[i] <= 1000
- nums 中的所有元素 互不相同
- 1 <= target <= 1000



### 思路

令`dp[i]`表示选取的元素之和等于`i`的方案数，结果就是`dp[target]`。

初始化`dp[0] = 1`，遍历`i`从1到`target`，当遇到`nums[i] < i`时，将`dp[i - nums[i]]`加到`dp[i]`上。



### 代码实现

```go
func combinationSum4(nums []int, target int) int {
    result := make([]int, target + 1)
    result[0] = 1
    for i := 1;i <= target;i++{
        for _,v := range nums{
            if(v <= i){
                result[i] += result[i - v]
            }
        }
    }
    return result[target]
}
```



