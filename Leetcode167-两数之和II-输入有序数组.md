---
title: Leetcode167.两数之和II-输入有序数组
date: 2020-07-20 14:29:20
categories: Leetcode
tags:
  - 双指针
  - 二分法
---

## Leetcode167.两数之和II-输入有序数组

给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 `index1` 和 `index2`，其中 `index1` 必须小于 `index2`。

说明:

返回的下标值（`index1` 和 `index2`）不是从零开始的。
你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

[题目链接](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted)

<!--more-->

示例:

```
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```



### 思路

- 二分法

  每次固定一个值，利用二分法从这个值的右边找到一个值`currentTarget`，其中`currentTarget = target- numbers[i]`。

- 双指针

  使用两个指针分别指向第一个元素位置和最后一个元素位置，计算两个指针指向的数字之和，如果小于`target`，左指针右移；如果大于`target`，右指针左移；如果相等，则唯一解找到。

  因为明确了有唯一解，所以用双指针不会遗漏答案。



### 代码实现

- 二分法

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        for(int i = 0;i<numbers.length-1;i++){
            //相当于在i的右侧找currentTarget
            int currentTarget = target - numbers[i];
            int left = i+1;
            int right = numbers.length-1;
            while(left<=right){
                int mid = left+(right-left)/2;
                if(numbers[mid]==currentTarget){
                    return new int[]{i+1,mid+1};
                }else if(numbers[mid]<currentTarget){
                    left = mid +1;
                }else{
                    right = mid - 1;
                }
            }
        }
        return new int[]{0,0};
    }
}
```

- 双指针

```jav
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int lo = 0;
        int hi = numbers.length-1;
        while(lo<hi){
            int sum = numbers[lo] + numbers[hi];
            if(sum==target){
                return new int[]{lo+1, hi+1};
            }else if(sum<target){
                lo +=1;
            }else{
                hi-=1;
            }
        }
        return new int[]{0,0};
    }
}
```

