---
title: Leetcode240.搜索二维矩阵II
date: 2020-11-14 10:54:35
category: Leetcode
tags:
  - 二分查找
---

## Leetcode240.搜索二维矩阵II

编写一个高效的算法来搜索 `m x n` 矩阵 `matrix `中的一个目标值 `target`。该矩阵具有以下特性：

每行的元素从左到右升序排列。
每列的元素从上到下升序排列。

[题目链接](https://leetcode-cn.com/problems/search-a-2d-matrix-ii)

<!--more-->

示例:

```
现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。
```



### 思路

因为矩阵每行从左到右升序，每列从上到下升序，所以可以从右上方或者左下方开始遍历，这样每次可以排除一行或者一列。

以右上方为例：

- 当target大于当前元素时，target一定出现在当前元素的下方，将行加一；
- 当target小于当前元素时，target一定出现在当前元素的左方，将列减一。



### 代码实现

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0){
            return false;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int i = 0;
        int j = n - 1;
        while(i < m && j >= 0){
            if(matrix[i][j] == target){
                return true;
                //排除一行
            }else if(matrix[i][j] < target){
                i++;
                //排除一列
            }else{
                j--;
            }
        }
        return false;
    }
}
```

