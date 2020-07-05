---
title: Leetcode448.找到所有数组中消失的数字
date: 2020-07-05 09:59:29
categories: Leetcode
tags:
  - Array
---

## Leetcode448.找到所有数组中消失的数字

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

[题目链接](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array)

<!--more-->

示例:

```
输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```



### 思路

因为数组中元素为`[1,n]`，所以可以进行原地修改进行标记。

遍历整个数组，将`Math.abs(nums[i])-1`处索引位置处的元素乘以-1置为负数。

然后再次遍历数组，若当前数组中元素为负数，则代表存在数字`i+1`，`i`为下标。



### 代码实现

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        for(int i = 0;i<nums.length;i++){
            int newIndex = Math.abs(nums[i])-1;
            if(nums[newIndex]>0){
                nums[newIndex] *=-1;
            }
        }
        List<Integer> result = new ArrayList<>();
        for(int i = 1;i<=nums.length;i++){
            if(nums[i-1]>0){
                result.add(i);
            }
        }
        return result;
    }
}
```

