---
title: Leetcode1.两数之和
date: 2020-10-03 10:19:23
categories: Leetcode
tags:
  - 哈希表
---

##  Leetcode1.两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

 [题目链接](https://leetcode-cn.com/problems/two-sum)

<!--more-->

示例:

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```



### 思路

1. 暴力枚举

   时间复杂度为`O(n^2)`。

2. 哈希表

   枚举法每次寻找`target-nums[i]`的复杂度太高，可以建立`nums`中元素与下标对应的哈希表降低复杂度。



### 代码实现

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[]{0, 0};
        if (nums == null || nums.length < 2) {
            return null;
        }
        Map<Integer, Integer> map = new HashMap<>(nums.length);
        for (int i = 0; i < nums.length; i++) {
            //从前往后枚举，如果有答案会出现重复，所以不使用先将所有元素入表
            if (map.containsKey(target-nums[i])){
                result[0] = i;
                result[1] = map.get(target-nums[i]);
                return result;
            }
            map.put(nums[i],i);
        }
        return result;
    }
}
```

