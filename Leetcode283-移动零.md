---
title: Leetcode283.移动零
date: 2020-06-29 17:47:36
categories: Leetcode
tags:
  - 双指针
---

## Leetcode283.移动零

给定一个数组 `nums`，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

[题目链接](https://leetcode-cn.com/problems/move-zeroes)

<!--more-->

示例:

```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```



说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。



### 思路

一次遍历，与快速排序切分`partition`相似，将非零元素移到左边，零元素移到右边。

声明两个指针`i`、`j`初始时指向0，遍历数组，当`nums[i]!=0`时，交换`nums[i]`与`nums[j]`，`j++`。

因此`j`也可以看成数组中非零元素的个数。



### 代码实现

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if(nums==null||nums.length<=1){
            return;
        }
        int n = nums.length;
        //i,j两个指针
        int j = 0;
        for(int i = 0;i<n;i++){
            //当出现非零元素时交换nums[i]与nums[j]
            if(nums[i]!=0){
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j++] = temp;
            }
        }
    }
}
```

