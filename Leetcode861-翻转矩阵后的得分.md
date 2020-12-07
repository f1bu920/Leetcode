---
title: Leetcode861.翻转矩阵后的得分
date: 2020-12-07 11:21:52
category: Leetcode
tags:
  - 贪心
---

## Leetcode861.翻转矩阵后的得分

有一个二维矩阵 A 其中每个元素的值为 0 或 1 。

移动是指选择任一行或列，并转换该行或列中的每一个值：将所有 0 都更改为 1，将所有 1 都更改为 0。

在做出任意次数的移动后，将该矩阵的每一行都按照二进制数来解释，矩阵的得分就是这些数字的总和。

返回尽可能高的分数。

 [题目链接](https://leetcode-cn.com/problems/score-after-flipping-matrix)

<!--more-->

示例：

```
输入：[[0,0,1,1],[1,0,1,0],[1,1,0,0]]
输出：39
解释：
转换为 [[1,1,1,1],[1,0,0,1],[1,1,1,1]]
0b1111 + 0b1001 + 0b1111 = 15 + 9 + 15 = 39
```




提示：

- 1 <= A.length <= 20
- 1 <= A[0].length <= 20
- `A[i][j]` 是 0 或 1



### 思路

1. 将第一列全部置为1
2. 从第一列开始，计算每一列中1的个数`count`，如果`count`小于列个数一半，将这一列翻转。
3. 计算这一列对结果的贡献，即`count * Math.pow(2, A[0].length - i - 1)`



### 代码实现

```java
class Solution {
    public int matrixScore(int[][] A) {
        int m = A.length;
        int n = A[0].length;
        for(int[] a : A){
            if(a[0] == 0){
                for(int i = 0;i < n;i++){
                    a[i] = 1 - a[i];
                }
            }
        }
        int result = 0;
        for(int i = 0;i < n;i++){
            int count = 0;
            for(int j = 0;j < m;j++){
                if(A[j][i] == 1){
                    count++;
                }
            }
            if(count <= A.length / 2){
                count = A.length - count;
            }
            result += count * Math.pow(2, n - i - 1);
        }
        return result;
    }
}
```

