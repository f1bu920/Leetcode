---
title: Leetcode368.最大整除子集
date: 2021-04-23 15:00:25
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode368.最大整除子集

给你一个由 无重复 正整数组成的集合 nums ，请你找出并返回其中最大的整除子集 answer ，子集中每一元素对 (answer[i], answer[j]) 都应当满足：
answer[i] % answer[j] == 0 ，或
answer[j] % answer[i] == 0
如果存在多个有效解子集，返回其中任何一个均可。

 [题目链接](https://leetcode-cn.com/problems/largest-divisible-subset)

<!--more-->

示例 1：

输入：nums = [1,2,3]
输出：[1,2]
解释：[1,3] 也会被视为正确答案。
示例 2：

输入：nums = [1,2,4,8]
输出：[1,2,4,8]


提示：

- 1 <= nums.length <= 1000
- 1 <= nums[i] <= 2 * 109
- nums 中的所有整数 互不相同



### 思路

`dp[i]`表示在升序条件下，以`nums[i]`为最大整数的最大整除子集的大小。枚举`[i, j]`区间，其中`0<=i<j`，如果`nums[j] % nums[i] == 0`，则`nums[i]`可以作为`nums[j]`最大整除子集中的一个元素。

因为最大整除自己不一定包含最大元素，所以从后往前枚举所有的`dp[i]`，选出最大整除子集的大小`maxSize`和该最大整除子集的最大值`maxVal`。倒叙遍历数组，如果`dp[i]==maxSize && maxVal % nums[i] == 0`，则将当前元素添加到结果集中，并更新`maxSize`和`maxVal`。



### 代码实现

```go
func largestDivisibleSubset(nums []int) []int {
	sort.Ints(nums)
	n := len(nums)
	dp := make([]int, n)
	for i := 0; i < n; i++ {
		dp[i] = 1
	}
	maxSize, maxVal := 1, nums[0]
	for j := 1; j < n; j++ {
		for i, v := range nums[:j] {
			if nums[j]%v == 0 {
				dp[j] = max(dp[j], dp[i]+1)
			}
		}
		if dp[j] > maxSize {
			maxSize, maxVal = dp[j], nums[j]
		}
	}
	if maxSize == 1 {
		return []int{nums[0]}
	}
	result := make([]int, maxSize)
	index := 0
	for i := n - 1; i >= 0; i-- {
		if dp[i] == maxSize && maxVal%nums[i] == 0 {
			result[index] = nums[i]
			index++
			maxVal = nums[i]
			maxSize--
		}
	}
	return result
}

func max(i, j int) int {
	if i >= j {
		return i
	} else {
		return j
	}
}
```



