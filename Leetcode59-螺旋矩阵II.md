---
title: Leetcode59.螺旋矩阵II
date: 2021-03-24 21:38:59
categories: Leetcode
tags:
  - Array
---

## Leetcode59.螺旋矩阵

给你一个正整数 n ，生成一个包含 1 到 n^2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 

示例 1：


输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
示例 2：

输入：n = 1
输出：[[1]]


提示：

1 <= n <= 20



### 思路及代码实现

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int top = 0;
        int bottom = n - 1;
        int left = 0;
        int right = n - 1;
        int num = 1;
        int[][] result = new int[n][n];
        while(true){
            for(int k = left;k <= right;k++){
                result[top][k] = num;
                num++;
            }
            if(++top > bottom){
                break;
            }
            for(int k = top;k <= bottom;k++){
                result[k][right] = num;
                num++;
            }
            if(--right < left){
                break;
            }
            for(int k = right;k >= left;k--){
                result[bottom][k] = num;
                num++;
            }
            if(--bottom < top){
                break;
            }
            for(int k = bottom;k >= top;k--){
                result[k][left] = num;
                num++;
            }
            if(++left > right){
                break;
            }
        }
        return result;
    }
}
```



