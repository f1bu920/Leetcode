---
title: Leetcode31.下一个排列
date: 2020-06-22 13:57:09
categories: Leetcode
tags:
  - Array
---

## Leetcode31.下一个排列

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

[题目链接](https://leetcode-cn.com/problems/next-permutation)

<!--more-->

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```



### 思路

下一个排列的定义是将给定数字序列按照字典序排成下一个更大的排列，如果没有更大的排列，就排成最小的即升序排列。如`12385764`的下一个更大的排列为`12386457`.

[参考思路](https://leetcode-cn.com/problems/next-permutation/solution/xia-yi-ge-pai-lie-suan-fa-xiang-jie-si-lu-tui-dao-/)

从后往前查找第一个相邻升序的元素对，其下标分别为`i`、`j`. 此时`nums[i]<nums[j]`且`[j, n-1]`上数组必定降序。

在`[j, n-1]`上从后往前找到第一个大于`nums[i]`的值，其下标记为`k`。

交换`nums[i]`和`nums[k]`，此时`[j, n-1]`一定降序，将`[j, n-1]`逆序排列。



### 代码实现

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;
        if (n <= 1) {
            return;
        }
        int i = n - 2;
        int j = n - 1;
        int k = n - 1;
        //从后往前找到第一个升序的元素对
        while (i >= 0 && nums[j] <= nums[i]) {
            i--;
            j--;
        }
        //i>=0代表此时不是最大排列
        if (i >= 0) {
            //从后往前找到第一个大于nums[i]的元素，其下标为k
            while (nums[k] <= nums[i]) {
                k--;
            }
            //交换nums[i]与nums[k]
            int temp = nums[i];
            nums[i] = nums[k];
            nums[k] = temp;
        }
        //此时[j, n-1]一定为逆序，将[j, n-1]逆序排列
        int lo = j, hi = n - 1;
        while (lo <= hi) {
            int temp = nums[lo];
            nums[lo] = nums[hi];
            nums[hi] = temp;
            lo++;
            hi--;
        }
    }
}
```

