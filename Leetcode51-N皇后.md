---
title: Leetcode51.N皇后
date: 2020-09-03 09:10:04
categories: Leetcode
tags:
  - 回溯
---

## Leetcode51.N皇后

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

![](https://f1bu920.github.io/images/8-queens.png)

上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

 [题目链接](https://leetcode-cn.com/problems/n-queens)

<!--more-->

示例：

```
输入：4
输出：[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```




提示：

皇后彼此不能相互攻击，也就是说：任何两个皇后都不能处于同一条横行、纵行或斜线上。



### 思路

[官方题解](https://leetcode-cn.com/problems/n-queens/solution/nhuang-hou-by-leetcode-solution/)

任何两个皇后不能再同一行、同一列和同一斜线上。将N个皇后放在N*N的棋盘上，所以每一行必定有一个皇后，所以可以利用回溯求解。

使用数组`queens`记录每行放置皇后的列下标，每次新放置的皇后都不能和以往的再同一行、同一列和同一斜线上，所以创建三个哈希表`columns`、`diagonals1`、`diagonals2`分别记录每一列以及两个方向的斜线上是否有皇后。`diagonals1`表示从左上到右下的斜线，斜线上的每个位置都满足**行下标与列下标之差相等；**

`diagonals2`表示从右上到左下的斜线，斜线上的每个位置都满足**行下标与列下标之和相等。**

每次放置皇后时判断位置是否在这三个哈希表中。



### 代码实现

```java
class Solution {
    List<List<String>> result = new ArrayList<>();
    //列
    Set<Integer> columns = new HashSet<>();
    //左上到右下的斜线
    Set<Integer> diagonals1 = new HashSet<>();
    //右上到左下的斜线
    Set<Integer> diagonals2 = new HashSet<>();

    public List<List<String>> solveNQueens(int n) {
        if (n == 0) {
            return result;
        }
        //queens[i]存储第i行放置的皇后列下标
        int[] queens = new int[n];
        Arrays.fill(queens, -1);
        backtrace(n, 0, queens);
        return result;
    }

    private void backtrace(int n, int row, int[] queens) {
        if (row == n) {
            //得到一个结果
            List<String> list = convertArrayToBoard(queens, n);
            result.add(list);
        } else {
            //第一行有n种选择
            for (int i = 0; i < n; i++) {
                if (columns.contains(i)) {
                    continue;
                }
                //行坐标与列坐标之差相等
                int diagonal1 = row - i;
                if (diagonals1.contains(diagonal1)) {
                    continue;
                }
                //行坐标与列坐标之和相等
                int diagonal2 = row + i;
                if (diagonals2.contains(diagonal2)) {
                    continue;
                }
                queens[row] = i;
                columns.add(i);
                diagonals1.add(diagonal1);
                diagonals2.add(diagonal2);
                //考虑下一行
                backtrace(n, row + 1, queens);
                //回溯，因为全局使用一份queens数组和哈希表，所以回溯时一定要回退
                queens[row] = -1;
                columns.remove(i);
                diagonals1.remove(diagonal1);
                diagonals2.remove(diagonal2);
            }
        }
    }
    //将queens数组转化为列表结果
    private List<String> convertArrayToBoard(int[] queens, int n) {
        List<String> board = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            char[] row = new char[n];
            Arrays.fill(row, '.');
            row[queens[i]] = 'Q';
            board.add(String.valueOf(row));
        }
        return board;
    }
}
```



