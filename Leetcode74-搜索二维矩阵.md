---
title: Leetcode74.搜索二维矩阵
date: 2021-03-30 08:50:21
categories: Leetcode
tags:
  - 二分搜索
---

## Leetcode74.搜索二维矩阵

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。

[题目链接](https://leetcode-cn.com/problems/search-a-2d-matrix/)

<!--more-->


示例 1：


输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
输出：true
示例 2：


输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
输出：false


提示：

m == matrix.length
n == matrix[i].length
1 <= m, n <= 100
-104 <= `matrix[i][j]`, target <= 104

### 思路

因为每行第一个元素大于前一行最后一个元素，且每行都是升序的，所以可以进行坐标变化变成一维递增序列，再进行二分查找。



### 代码实现

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;
        int left = 0;
        int right = m * n - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            int value = matrix[mid / n][mid % n];
            if(target == value){
                return true;
            }else if(value > target){
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return false;
    }
}
```

