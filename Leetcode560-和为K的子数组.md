---
title: Leetcode560.和为K的子数组
date: 2020-05-15 08:12:12
categories: Leetcode
tags:
  - 数组
  - 前缀和
---

## Leetcode560.和为K的子数组

给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

[题目链接](https://leetcode-cn.com/problems/subarray-sum-equals-k)

<!--more-->

示例 1 :

输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
说明 :

数组的长度为 [1, 20,000]。
数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]。

#### 思路

- 暴力法

  确定左边界，枚举有边界，若和`sum==k`，则计数器`count++`。

- 前缀和

  创建前缀和数组`preSum[len+1]`，并初始化令`preSum[0]=0`，前缀和数组`preSum[i]`的语意为`nums[0]`到`nums[i-1]`的和。**注意这里有一位的下标偏移。**

  枚举子数组左右边界，当右边界+1的前缀和减去左边界的前缀和等于目标值时，计数器加一。



#### 代码实现

- 暴力法

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        int len = nums.length;
        for (int left = 0; left < len; left++) {
            int sum = 0;
            for (int i = left; i < len; i++) {
                sum += nums[i];
                if (sum == k) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

- 前缀和

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        int len = nums.length;
        int[] preSum = new int[len + 1];
        preSum[0] = 0;
        for (int i = 0; i < len; i++) {
            preSum[i + 1] = preSum[i] + nums[i];
        }
        for (int left = 0; left < len; left++) {
            for (int right = left; right < len; right++) {
                //注意这里的下标偏移，可带入left=0检验
                if (preSum[right + 1] - preSum[left] == k) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

