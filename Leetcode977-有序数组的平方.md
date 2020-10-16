---
title: Leetcode977.有序数组的平方
date: 2020-10-16 09:55:03
categories: Leetcode
tags:
  - 双指针
---

## Leetcode977.有序数组的平方

给定一个按非递减顺序排序的整数数组 A，返回每个数字的平方组成的新数组，要求也按非递减顺序排序。

 [题目链接](https://leetcode-cn.com/problems/squares-of-a-sorted-array)

<!--more-->

示例 1：

```
输入：[-4,-1,0,3,10]
输出：[0,1,9,16,100]
```



示例 2：

```
输入：[-7,-3,2,3,11]
输出：[4,9,9,49,121]
```




提示：

- 1 <= A.length <= 10000
- -10000 <= A[i] <= 10000
- A 已按非递减顺序排序。



### 思路

利用两个指针`left`和`right`分别指向数组两端，每次判断两者的绝对值那个更大，更大的添加到结果中。



### 代码实现

```java
class Solution {
    public int[] sortedSquares(int[] A) {
        int[] result = new int[A.length];
        int left = 0;
        int right = A.length-1;
        for(int i = right;i>=0;i--){
            if(Math.abs(A[left])>=Math.abs(A[right])){
                result[i] = A[left]*A[left];
                left++;
            }else{
                result[i] = A[right]*A[right];
                right--;
            }
        }
        return result;
    }
}
```



