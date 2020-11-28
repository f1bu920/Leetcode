---
title: Leetcode493.翻转对
date: 2020-11-28 11:03:24
category: Leetcode
tags:
  - 归并排序
  - 二分查找
---

## Leetcode493.翻转对

给定一个数组 `nums` ，如果 `i < j` 且 `nums[i] > 2*nums[j]` 我们就将 `(i, j)` 称作一个重要翻转对。

你需要返回给定数组中的重要翻转对的数量。

[题目链接](https://leetcode-cn.com/problems/reverse-pairs)

<!--more-->

示例 1:

```
输入: [1,3,2,3,1]
输出: 2
```



示例 2:

```
输入: [2,4,3,5,1]
输出: 3
```



注意:

- 给定数组的长度不会超过50000。
- 输入数组中的所有数字都在32位整数的表示范围内。



### 思路

对于数组`nums[left,..right]`，分别求出子数组`nums[left,mid]`和`nums[mid + 1, right]`的翻转对数目并将两个子数组排好序，则数组`nums[left,right]`中的翻转对数目等于两个子数组翻转对之和加上左右端点分别位于两个子数组的翻转对数量。

在两个子数组中分别维护指针i，j，不断向右移动j直到`nums[i] <= 2 * nums[j]`，此时以`i`为左端点的翻转对数量为`j - mid - 1`，再将`i`右移直到`i > mid`。



### 代码实现

```java
class Solution {
    public int reversePairs(int[] nums) {
        if (nums == null || nums.length < 2) {
            return 0;
        }
        return reversePairs(nums, 0, nums.length - 1);
    }

    private int reversePairs(int[] nums, int left, int right) {
        if (left >= right) {
            return 0;
        } else {
            int mid = left + (right - left) / 2;
            int n1 = reversePairs(nums, left, mid);
            int n2 = reversePairs(nums, mid + 1, right);
            int result = n1 + n2;
            int i = left;
            int j = mid + 1;
            //统计两端点分为在两个子数组中的翻转对数量
            while (i <= mid) {
                while (j <= right && (long) nums[i] > 2 * (long) nums[j]) {
                    j++;
                }
                result += j - mid - 1;
                i++;
            }
            //进行归并排序
            int[] temp = new int[right - left + 1];
            int index1 = left;
            int index2 = mid + 1;
            int k = 0;
            while (index1 <= mid || index2 <= right) {
                if (index1 > mid) {
                    temp[k++] = nums[index2++];
                } else if (index2 > right) {
                    temp[k++] = nums[index1++];
                } else {
                    if (nums[index1] < nums[index2]) {
                        temp[k++] = nums[index1++];
                    } else {
                        temp[k++] = nums[index2++];
                    }
                }
            }
            for (int t = 0; t < temp.length; t++) {
                nums[left + t] = temp[t];
            }
            return result;
        }
    }
}
```



