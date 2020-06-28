---
title: Leetcode209.长度最小的子数组
date: 2020-06-28 09:04:29
categories: Leetcode
tags:
  - 双指针
  - Slide Window
---

## Leetcode209.长度最小的子数组

给定一个含有 `n` 个正整数的数组和一个正整数 `s` ，找出该数组中满足其和 `≥ s` 的长度最小的连续子数组，并返回其长度。如果不存在符合条件的连续子数组，返回 0。

[题目链接](https://leetcode-cn.com/problems/minimum-size-subarray-sum)

<!--more-->

示例: 

```
输入: s = 7, nums = [2,3,1,2,4,3]
输出: 2
解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。
```



进阶:

如果你已经完成了O(n) 时间复杂度的解法, 请尝试 O(n log n) 时间复杂度的解法。



### 思路

利用双指针`start`和`end`，初始时都指向`0`。利用变量`sum`记录当前窗口的数组和。每次循环中先将`end`指向的数组元素加到`sum`中，若此时`sum>=s`，更新最小长度，将`start`指针右移，同时`sum`中减去`nums[start]`，直到`sum<s`。最后右移`end`，循环上述过程。



### 代码实现

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int n = nums.length;
        int minLen = Integer.MAX_VALUE;
        int start = 0, end = 0;
        int sum = 0;
        while (end < n) {
            sum += nums[end];
            while (sum >= s) {
                minLen = Math.min(minLen, end - start + 1);
                sum -= nums[start];
                start++;
            }
            end++;
        }
        return minLen == Integer.MAX_VALUE ? 0 : minLen;
    }
}
```



