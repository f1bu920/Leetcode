---
title: Leetcode4.寻找两个正序数组的中位数
date: 2020-05-24 10:39:28
categories: Leetcode
tags:
  - 二分查找
  - 双指针
---

## Leetcode4.寻找两个正序数组的中位数

给定两个大小为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。

请你找出这两个正序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

 [题目链接](https://leetcode-cn.com/problems/median-of-two-sorted-arrays)

<!--more-->

示例 1:

```
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
```

示例 2:

```
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

#### 思路及代码实现

- 已知两个数组长度，且两个数组为有序数组，则可以通过两个指针找到中位数所在的位置。两个数组长度和为`m+n`，`m+n`是奇数时，中位数为合并后的下标为`(m+n)/2`处；为偶数时，需要知道两个值，下标为`(m+n)/2`和`(m+n)/2 - 1`。

  所以我们需要两个值，当前遍历的值`curVal`和上次遍历的值`preVal`，奇数个时，中位数为`curVal`，偶数个时，中位数为`(curVal+preVal)/2.0`。

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        //特判，有一个数组为空的情况
        if (nums1 == null || nums1.length == 0) {
            int len = nums2.length;
            return len % 2 == 1 ? nums2[len / 2] : (nums2[len / 2] + nums2[len / 2 - 1]) / 2.0;
        }
        if (nums2 == null || nums2.length == 0) {
            int len = nums1.length;
            return len % 2 == 1 ? nums1[len / 2] : (nums1[len / 2] + nums1[len / 2 - 1]) / 2.0;
        }
        int m = nums1.length;
        int n = nums2.length;
        //两个指针
        int point1 = 0;
        int point2 = 0;
        //当前的值
        int curVal = 0;
        //上次遍历的值
        int preVal = 0;
        //注意这里是<=
        for (int i = 0; i <= (m + n) / 2; i++) {
            //赋值
            preVal = curVal;
            //数组一遍历完情况
            if (point1 == m) {
                curVal = nums2[point2++];
                //数组二遍历完情况
            } else if (point2 == n) {
                curVal = nums1[point1++];
                //较小值的数组指针指向下一位
            } else if (nums1[point1] <= nums2[point2]) {
                curVal = nums1[point1++];
            } else {
                curVal = nums2[point2++];
            }
        }
        //奇数情况
        if ((m + n) % 2 == 1) {
            return curVal;
        } else
            //偶数情况
            return (preVal + curVal) / 2.0;
    }
}
```

上述我自己的代码时间复杂度为`O(m+n)`，要求时间复杂度为`O(log(m+n))`的话可以参考官方题解：[官方题解](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xun-zhao-liang-ge-you-xu-shu-zu-de-zhong-wei-s-114/)

