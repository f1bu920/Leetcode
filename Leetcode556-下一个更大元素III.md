---
title: Leetcode556.下一个更大元素III
date: 2022-07-03 19:47:09
categories: Leetcode
tags:
  - 双指针
---

## Leetcode556.下一个更大元素III

给你一个正整数 `n` ，请你找出符合条件的最小整数，其由重新排列 `n` 中存在的每位数字组成，并且其值大于 `n` 。如果不存在这样的正整数，则返回 -1 。

注意 ，返回的整数应当是一个 32 位整数 ，如果存在满足题意的答案，但不是 32 位整数 ，同样返回 -1 。

 [原题链接](https://leetcode.cn/problems/next-greater-element-iii)

<!--more-->

示例 1：

```java
输入：n = 12
输出：21
```



示例 2：

```java
输入：n = 21
输出：-1
```




提示：

- `1 <= n <= 2^32 - 1`



### 思路

本题是在[Leetcode31.下一个排列](https://leetcode.cn/problems/next-permutation/)基础上的修改，先从后往前遍历找到第一个相邻升序对`nums[i]、nums[j]，i>j`，此时可知从`j`到`len-1`是降序排列的；再从后往前查找，找到第一个位置`k`使得`nums[k]>nums[i]`，交换`nums[i]`与`nums[k]`，则可知`[j, len-1]`一定降序，将`[j, len-1]`逆序排列。



### 实现

```java
class Solution {
   public int nextGreaterElement(int n) {
        if (n < 10) {
            return -1;
        }
        char[] nums = Integer.toString(n).toCharArray();
        int len = nums.length;
        int i = len - 2;
       // 从后往前查找第一个升序对
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }
       // 如果没找到，说明已经是最大值了
        if (i < 0) {
            return -1;
        }
       // 从后往前查找第一个大于nums[i]的位置
        int j = len - 1;
        while (j >= 0 && nums[i] >= nums[j]) {
            j--;
        }
       // 交换位置
        swap(nums, i, j);
       // 从i+1到len-1是降序的，要找下一个更大元素因此将其逆序排列
        int begin = i + 1;
        int end = len - 1;
        while (begin < end) {
            swap(nums, begin, end);
            begin++;
            end--;
        }
       // 判断是否超过int范围
        long result = Long.parseLong(new String(nums));

        return result > Integer.MAX_VALUE ? -1 : (int) result;
    }

    public void swap(char[] nums, int i, int j) {
        char temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

