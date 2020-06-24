---
title: Leetcode面试题29.顺时针打印矩阵
date: 2020-06-05 09:27:40
categories: Leetcode
tags:
  - Array
  - 模拟
---

## Leetcode面试题29.顺时针打印矩阵

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

 [题目链接](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof)

<!--more-->

示例 1：

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```



示例 2：

```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```




限制：

- 0 <= matrix.length <= 100
- 0 <= matrix[i].length <= 100



#### 思路

设定矩阵的四个边界，初始化时上边界`top=0`，下边界`bottom=matrix.length-1`，左边界`left=0`，右边界`right=matrix[0].length-1`。模拟顺时针打印。

循环打印，将元素添加到`result`尾部，边界向内收缩，判断是否相遇，相遇则代表打印完毕。



#### 代码实现

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return new int[0];
        }
        int row = matrix.length;
        int col = matrix[0].length;
        int[] result = new int[row * col];
        int x = 0;
        int left = 0, right = matrix[0].length - 1;
        int top = 0, bottom = matrix.length - 1;
        while (true) {
            for (int i = left; i <= right; i++) {
                result[x++] = matrix[top][i];
            }
            //上边界向下收缩
            if (++top > bottom) {
                break;
            }
            for (int i = top; i <= bottom; i++) {
                result[x++] = matrix[i][right];
            }
            //右边界向左收缩
            if (--right < left) {
                break;
            }
            for (int i = right; i >= left; i--) {
                result[x++] = matrix[bottom][i];
            }
            //下边界向上收缩
            if (--bottom < top) {
                break;
            }
            for (int i = bottom; i >= top; i--) {
                result[x++] = matrix[i][left];
            }
            //左边界向右收缩
            if (++left > right) {
                break;
            }
        }
        return result;
    }
}
```



