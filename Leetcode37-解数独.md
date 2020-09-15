---
title: Leetcode37.解数独
date: 2020-09-15 09:46:42
categories: Leetcode
tags:
  - 回溯
---

## Leetcode37.解数独

编写一个程序，通过已填充的空格来解决数独问题。

一个数独的解法需遵循如下规则：

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。
空白格用 '.' 表示。

![](https://f1bu920.github.io/images/Leetcode37.解数独1.jpg)

一个数独。

![](https://f1bu920.github.io/images/Leetcode37.解数独2.jpg)

答案被标成红色。

[题目链接](https://leetcode-cn.com/problems/sudoku-solver)

<!--more-->

Note:

- 给定的数独序列只包含数字 1-9 和字符 '.' 。
- 你可以假设给定的数独只有唯一解。
- 给定数独永远是 9x9 形式的。



### 思路

因为每一行只能出现一次数字1-9，每一列只能出现一次数字1-9，每一个块只能出现一次数字1-9，所以可以创建`rows[i][j]`记录第i行数字j+1是否出现过，`cols[i][j]`记录第i列数字j+1是否出现过，`blocks[i/3][j/3][k]`表示第i行、第j列所在的块中数字k是否出现过。

使用全局变量`valid`记录是否正确。



### 代码实现

```java
class Solution {
    boolean[][] rows = new boolean[9][9];
    boolean[][] cols = new boolean[9][9];
    //记录需要填入数字的坐标
    List<int[]> list = new ArrayList();
    boolean[][][] blocks = new boolean[3][3][9];
    boolean valid = false;

    public void solveSudoku(char[][] board) {
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') {
                    list.add(new int[]{i, j});
                } else {
                    int digit = board[i][j] - '1';
                    rows[i][digit] = true;
                    cols[j][digit] = true;
                    blocks[i / 3][j / 3][digit] = true;
                }
            }
        }
        dfs(board, 0);
    }

    private void dfs(char[][] board, int position) {
        if (position == list.size()) {
            //遍历完成，找到了正确答案
            valid = true;
            return;
        }
        for (int digit = 0; digit < 9 && !valid; digit++) {
            int[] pos = list.get(position);
            int i = pos[0];
            int j = pos[1];
            //行、列、块中均未出现此数字
            if (!rows[i][digit] && !cols[j][digit] && !blocks[i / 3][j / 3][digit]) {
                rows[i][digit] = true;
                cols[j][digit] = true;
                blocks[i / 3][j / 3][digit] = true;
                board[i][j] = (char) (digit + '1');
                dfs(board, position + 1);
                //回溯
                rows[i][digit] = false;
                cols[j][digit] = false;
                blocks[i / 3][j / 3][digit] = false;
            }
        }
    }
}
```

