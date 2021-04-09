---
title: Leetcode80.删除有序数组中的重复项II
date: 2021-04-08 10:32:35
categories: Leetcode
tags:
  - 双指针
---

## Leetcode80.删除有序数组中的重复项II

给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使每个元素 最多出现两次 ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

 [题目链接](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii)

<!--more-->

说明：

为什么返回数值是整数，但输出的答案是数组呢？

请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}


示例 1：

输入：nums = [1,1,1,2,2,3]
输出：5, nums = [1,1,2,2,3]
解释：函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。 不需要考虑数组中超出新长度后面的元素。
示例 2：

输入：nums = [0,0,1,1,1,1,2,3,3]
输出：7, nums = [0,0,1,1,2,3,3]
解释：函数应返回新长度 length = 7, 并且原数组的前五个元素被修改为 0, 0, 1, 1, 2, 3, 3 。 不需要考虑数组中超出新长度后面的元素。


提示：

- 1 <= nums.length <= 3 * 104
- -104 <= nums[i] <= 104
- nums 已按升序排列



### 思路

慢指针`j`表示处理后数组的长度，快指针`i`表示当前遍历的数组的下标。当`nums[i] != nums[j - 2]`时，将`nums[i]`赋给`nums[j]`同时将`j`右移一位。



### 代码实现

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        //长度小于等于2直接返回
        if(nums.length <= 2){
            return nums.length;
        }
        //j指向处理后数组最后一位下标
        int j = 2;
        for(int i = 2;i < nums.length;i++){
            //因为是排序数组，如果nums[i] == nums[j - 2]必定会出现三个以上的连续数字
            if(nums[i] != nums[j - 2]){
                nums[j++] = nums[i];
            }
        }
        return j;
    }
}
```





