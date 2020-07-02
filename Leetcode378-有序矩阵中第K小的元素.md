---
title: Leetcode378.有序矩阵中第K小的元素
date: 2020-07-02 09:05:16
categories: Leetcode
tags:
  - 堆
  - 优先级队列
---

## Leetcode378.有序矩阵中第K小的元素

给定一个 n x n 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第 k 小的元素。
请注意，它是排序后的第 k 小元素，而不是第 k 个不同的元素。

 [题目链接](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix)

<!--more-->

示例：

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

返回 13。
```



提示：
你可以假设 k 的值永远是有效的，1 ≤ k ≤ n2 。



### 思路

与合并多个有序链表类似，可以利用优先级队列来解决。因为矩阵中每行数组都是有序的，因此可以看成合并这`n`个有序数组到第`k`个元素时停止。初始时将每个数组中的第一个元素入队，同时在同一个节点中存储这个元素所在的行和列数。**注意利用lambda表达式构造数组的排序规则，按照第一个元素升序排列。**

每次出队一个元素，如果这个元素不是其所在行的最后一个元素，则将其下一个元素入队。如此进行`k-1`次，最后返回第`k`次结果。



### 代码实现

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        //按照数组第一个元素升序排列
        PriorityQueue<int[]> queue = new PriorityQueue<>(n, (a, b) -> {
            return a[0] - b[0];
        });
        //先将所有行的第一个元素入队
        for (int i = 0; i < n; i++) {
            //i代表其所在行下标，0代表其列下标
            queue.offer(new int[]{matrix[i][0], i, 0});
        }
        for (int i = 0; i < k - 1; i++) {
            int[] poll = queue.poll();
            int row = poll[1];
            int col = poll[2];
            //如果不是这一行的最后一个元素，则入队其下一个元素
            if (col != n - 1) {
                queue.offer(new int[]{matrix[row][col + 1], row, col + 1});
            }
        }
        int[] kthSmall = queue.poll();
        return kthSmall[0];
    }
}
```



