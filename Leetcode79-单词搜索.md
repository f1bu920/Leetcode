---
title: Leetcode79.单词搜索
date: 2020-09-13 09:48:23
categories: Leetcode
tags:
  - 回溯
---

## Leetcode79.单词搜索

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 [题目链接](https://leetcode-cn.com/problems/word-search)
<!--more-->

示例:

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
```




提示：

- board 和 word 中只包含大写和小写英文字母。
- 1 <= board.length <= 200
- 1 <= board[i].length <= 200
- 1 <= word.length <= 10^3

### 思路

定义偏移量数组`directions`，每次dfs时传入横坐标、纵坐标和匹配单词下标。

遇到不匹配的情况进行回溯

### 代码实现

```java
class Solution {
    boolean[][] used;
    int[][] directions = new int[][]{{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

    public boolean exist(char[][] board, String word) {
        int rows = board.length;
        int cols = board[0].length;
        char[] ch = word.toCharArray();
        used = new boolean[rows][cols];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (dfs(i, j, 0, board, ch)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    private boolean dfs(int i, int j, int start, char[][] board, char[] ch) {
        //递归终止条件
        if (start == ch.length - 1) {
            return board[i][j] == ch[start];
        }
        if (board[i][j] == ch[start]) {
            used[i][j] = true;
            for (int k = 0; k < 4; k++) {
                int newRow = i + directions[k][0];
                int newCol = j + directions[k][1];
                if (newRow >= 0 && newRow < board.length && newCol >= 0 && newCol < board[0].length && !used[newRow][newCol]) {
                    if (dfs(newRow, newCol, start + 1, board, ch)) {
                        return true;
                    }
                }
            }
            //不匹配的情况，记得回溯
            used[i][j] = false;
        }
        return false;
    }
}
```

