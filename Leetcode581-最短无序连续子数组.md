---
title: Leetcode581.最短无序连续子数组
date: 2020-07-08 09:39:05
categories: Leetcode
tags:
  - Array
---

## Leetcode581.最短无序连续子数组

给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是最短的，请输出它的长度。

[题目链接](https://leetcode-cn.com/problems/shortest-unsorted-continuous-subarray)

<!--more-->

示例 1:

```
输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
```

说明 :

输入的数组长度范围在 [1, 10,000]。
输入的数组可能包含重复元素 ，所以升序的意思是<=。



### 思路

使用`clone()`方法复制一个数组`numsCopy`，将复制数组排序，然后遍历数组进行比较，找到最短无序长度。

时间复杂度为`O(nlogn)`，空间复杂度为`O(n)`。

### 代码实现

```java
class Solution {
    public int findUnsortedSubarray(int[] nums) {
        int[] numsCopy = nums.clone();
        Arrays.sort(numsCopy);
        int l = nums.length - 1;
        int r = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != numsCopy[i]) {
                l = Math.min(l, i);
                r = Math.max(r, i);
            }
        }
        return r > l ? r - l + 1 : 0;
    }
}
```

