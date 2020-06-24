---
title: Leetcode15.三数之和
date: 2020-05-23 14:45:51
categories: Leetcode
tags:
  - 双指针
---

## Leetcode15.三数之和

给你一个包含 n 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 [题目链接](https://leetcode-cn.com/problems/3sum)

<!--more-->

示例：

```
给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

#### 思路

1. 对数组进行排序
2. 遍历排序后数组。
   1. 若`nums[i]>0`，则比不可能有三数和为0，直接返回结果。
   2. 对于重复元素，跳过。
   3. 令左指针`l = i+1`，右指针`r=nums.length()-1`，当`l<r`时循环：
      - 当三数和`nums[i]+nums[l]+nums[r]==0`时，添加进集合；然后跳过左边界和右边界的重复元素。
      - 若三数和大于0，右边界左移。
      - 若三数和小于0，左边界右移。



#### 代码实现

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new LinkedList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            //此时不可能有三数和为0的情况，直接返回
            if (nums[i] > 0) {
                return result;
            }
            //去除重复元素
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            //左指针
            int l = i + 1;
            //右指针
            int r = nums.length - 1;
            while (l < r) {
                //三数和为0
                if (nums[i] + nums[l] + nums[r] == 0) {
                    List<Integer> list = new LinkedList<>();
                    list.add(nums[i]);
                    list.add(nums[l]);
                    list.add(nums[r]);
                    result.add(list);
                    //去除左右边界的重复
                    while (l < r && nums[l] == nums[l + 1]) {
                        l++;
                    }
                    while (l < r && nums[r] == nums[r - 1]) {
                        r--;
                    }
                    l++;
                    r--;
                    //三数和大于0.右边界左移
                } else if (nums[i] + nums[l] + nums[r] > 0) {
                    r--;
                } else {
                    //三数和小于0，左边界右移
                    l++;
                }
            }
        }
        return result;
    }
}
```

