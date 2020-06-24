---
title: Leetcode16.最接近的三数之和
date: 2020-06-24 09:32:18
categories: Leetcode
tags:
  - 双指针
---

## Leetcode16.最接近的三数之和

给定一个包括 `n` 个整数的数组 `nums` 和 一个目标值 `target`。找出 `nums` 中的三个整数，使得它们的和与 `target` 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

 [题目链接](https://leetcode-cn.com/problems/3sum-closest)

<!--more-->

示例：

```
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
```




提示：

- 3 <= nums.length <= 10^3
- -10^3 <= nums[i] <= 10^3
- -10^4 <= target <= 10^4



### 思路

排序后利用双指针进行枚举，外层循环`i`从0到`n-3`进行枚举，内层循环使用双指针`left`和`right`分别从两侧进行枚举。使用`closestNum`记录最接近`target`的和，使用`distance`记录距离`target`的最短距离，并在循环中更新这两个值。



### 代码实现

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        int closestNum = nums[0] + nums[1] + nums[2];
        int distance = Math.abs(closestNum - target);
        for (int i = 0; i < n - 2; i++) {
            int left = i + 1;
            int right = n - 1;
            while (left < right) {
                //当前和
                int temp = nums[i] + nums[left] + nums[right];
                if (temp < target) {
                    if (Math.abs(temp - target) < distance) {
                        distance = Math.abs(temp - target);
                        closestNum = temp;
                    }
                    left++;
                } else if (temp > target) {
                    if (Math.abs(temp - target) < distance) {
                        distance = Math.abs(temp - target);
                        closestNum = temp;
                    }
                    right--;
                } else {
                    return target;
                }
            }
        }
        return closestNum;
    }
}
```

