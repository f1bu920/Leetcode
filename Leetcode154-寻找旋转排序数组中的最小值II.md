---
title: Leetcode154.寻找旋转排序数组中的最小值II
date: 2021-04-09 09:49:48
categories: Leetcode
tags:
  - 二分查找
---

## Leetcode154.寻找旋转排序数组中的最小值II

已知一个长度为 n 的数组，预先按照升序排列，经由 1 到 n 次 旋转 后，得到输入数组。例如，原数组 nums = [0,1,4,4,5,6,7] 在变化后可能得到：
若旋转 4 次，则可以得到 [4,5,6,7,0,1,4]
若旋转 7 次，则可以得到 [0,1,4,4,5,6,7]
注意，数组 [a[0], a[1], a[2], ..., a[n-1]] 旋转一次 的结果为数组 [a[n-1], a[0], a[1], a[2], ..., a[n-2]] 。

给你一个可能存在 重复 元素值的数组 nums ，它原来是一个升序排列的数组，并按上述情形进行了多次旋转。请你找出并返回数组中的 最小元素 。

 [题目链接](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii)

<!--more-->

示例 1：

输入：nums = [1,3,5]
输出：1
示例 2：

输入：nums = [2,2,2,0,1]
输出：0


提示：

- n == nums.length
- 1 <= n <= 5000
- -5000 <= nums[i] <= 5000
- nums 原来是一个升序排序的数组，并进行了 1 至 n 次旋转



### 思路

二分法，当`mid`后边有序时，代表最小元素在`mid`及其左侧；否则最小值在`mid`右侧。

当`left == right`时唯一确定一个元素，所以循环退出条件为`left < right`。

因为存在重复元素，所以当`nums[mid] == nums[right] && nums[mid] == nums[left]`时无法确定区间，所以此时直接将`right--`、`left++`。



### 代码实现

```java
class Solution {
    public int findMin(int[] nums) {
        if(nums.length == 0){
            return nums[0];
        }
        int left = 0;
        int right = nums.length - 1;
        while(left < right){
            int mid = left + (right - left) / 2;
            if(nums[mid] == nums[left] && nums[mid] == nums[right]){
                left++;
                right--;
                continue;
            }
            if(nums[mid] <= nums[right]){
                right = mid;
            }else{
                left = mid + 1;
            }
        }
        return nums[left];
    }
}
```



