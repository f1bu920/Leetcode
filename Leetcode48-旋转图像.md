---
title: Leetcode48.旋转图像
date: 2020-07-24 20:51:38
categories: Leetcode
tags:
  - Array
---

## Leetcode48.旋转图像

给定一个 n × n 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

说明：

你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

[题目链接](https://leetcode-cn.com/problems/rotate-image)

<!--more-->

示例 1:

```
给定 matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

原地旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```



示例 2:

```
给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```



### 思路

使用矩阵右上到左下的对角线，将与对角线对称的元素进行交换，例如

`[
  [1,2,3],
  [4,5,6],
  [7,8,9]
]`，得到的结果就是`[
  [7,8,9],
  [4,5,6],
  [1,2,3]
],`再将矩阵的行进行交换就是结果。



### 代码实现

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for(int i = 0;i<n;i++){
            for(int j = 0;j<n-i;j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[n-j-1][n-i-1];
                matrix[n-j-1][n-i-1] = temp;
            }
        }
        for(int i = 0;i<n/2;i++){
            int[] temp = matrix[i];
            matrix[i] = matrix[n-i-1];
            matrix[n-1-i] = temp;
        }
    }
}
```



