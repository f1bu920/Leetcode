---
title: 剑指 Offer 03. 数组中重复的数字
date: 2022-07-02 18:41:43
categories: Leetcode
tags:
  - Array
---

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

[原题链接](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof)

<!--more-->

示例 1：

```java
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```




限制：

- 2 <= n <= 100000

## 思路

- 思路一

  利用Set存储元素，遍历时判断set中是否已经出现过，时间复杂度`O(n)`，空间复杂度`O(n)`。

- 思路二

  原地交换，在一个长度为 n 的数组 nums 里的所有数字都在 0 ~ n-1 的范围内，代表数组元素的索引与值是一对多的关系，可遍历数组并通过交换操作，使元素的 **索引** 与 **值** 一一对应（即 `nums[i] = i `）。遍历时，第一次遇到`x`，将其交换到索引为`x`处，第二次再遇到时一定代表一组重复数字。

## 实现

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        int i = 0;
        while(i < nums.length) {
            if(nums[i] == i) {
                i++;
                continue;
            }
            if(nums[nums[i]] == nums[i]) return nums[i];
            int tmp = nums[i];
            nums[i] = nums[tmp];
            nums[tmp] = tmp;
        }
        return -1;
    }
}
```

