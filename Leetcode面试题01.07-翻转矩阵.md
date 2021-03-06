---
title: Leetcode面试题01.07.翻转矩阵
date: 2020-04-09 10:43:17
categories: Leetcode
tags:
  - Math
  - Array
---

## Leetcode面试题01.07.旋转矩阵

给你一幅由 N × N 矩阵表示的图像，其中每个像素的大小为 4 字节。请你设计一种算法，将图像旋转 90 度。

不占用额外内存空间能否做到？

 [题目链接](https://leetcode-cn.com/problems/rotate-matrix-lcci)

<!--more-->

示例 1:

>给定 matrix = 
>[
>  [1,2,3],
>  [4,5,6],
>  [7,8,9]
>],
>
>原地旋转输入矩阵，使其变为:
>[
>  [7,4,1],
>  [8,5,2],
>  [9,6,3]
>]

示例 2:

>给定 matrix =
>[
>  [ 5, 1, 9,11],
>  [ 2, 4, 8,10],
>  [13, 3, 6, 7],
>  [15,14,12,16]
>], 
>
>原地旋转输入矩阵，使其变为:
>[
>  [15,13, 2, 5],
>  [14, 3, 4, 1],
>  [12, 6, 8, 9],
>  [16, 7,10,11]
>]

#### 思路及代码实现

- 借助辅助数组

  > 对于矩阵中第 i 行的第 j 个元素，在旋转后，它出现在倒数第 i 列的第 j 个位置。 

  我们将其翻译成代码。由于矩阵中的行列从 00 开始计数，因此对于矩阵中的元素 `temp[i][j]`，旋转后他的新位置为`matrix[j][N-i-1]`。

  ```java
  class Solution {
      public void rotate(int[][] matrix) {
          int N = matrix.length;
          int[][] temps = new int[N][N];
          for (int i = 0; i < N; i++) {
              for (int j = 0; j < N; j++) {
                  temps[i][j] = matrix[i][j];
              }
          }
          for (int i = 0; i < N; i++) {
              for (int j = 0; j < N; j++) {
                  matrix[j][N - i - 1] = temps[i][j];
              }
          }
      }
  }
  ```

  

- 用翻转代替旋转

  > 5  1  9 11
  > 2  4  8 10
  >13  3  6  7
  >15 14 12 16

  作为例子，先将其通过水平轴翻转得到：

  > 5  1  9 11                 15 14 12 16
  > 2  4  8 10                 13  3  6  7
  >------------   =水平翻转=>   ------------
  >13  3  6  7                  2  4  8 10
  >15 14 12 16                  5  1  9 11

  再根据主对角线 \ 翻转得到：

  >15 14 12 16                   		15 13  2  5
  >13  3  6  7   =主对角线翻转=>       14  3  4  1
  > 2  4  8 10                   			12  6  8  9
  > 5  1  9 11                   			16  7 10 11

  对于水平翻转，我们只需要枚举上半部分元素与下半部分元素进行交换。

  `matrix[row][col] = matrix[N-row-1][col]`

  对于主对角线翻转，只需要枚举对角线左侧元素与右侧进行交换。

  `matrix[row][col] = matrix[col][row]`.

  代码实现略。

  