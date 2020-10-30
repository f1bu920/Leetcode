---
title: Leetcode463.岛屿的周长
date: 2020-10-30 10:55:16
categories: Leetcode
tags:
 - 深度优先搜索
---

## Leetcode463.岛屿的周长

给定一个包含 0 和 1 的二维网格地图，其中 1 表示陆地 0 表示水域。

网格中的格子水平和垂直方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。

岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

 [题目链接](https://leetcode-cn.com/problems/island-perimeter)

<!--more-->

示例 :

```
输入:
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

输出: 16
```



### 思路

深度优先遍历，对于每个陆地格子的每条边，如果这条边作为棋盘的边界或者相邻的格子为水域时，这条边的贡献为1。记得遍历过的格子要置为2，防止重复遍历。



### 代码实现

```java
class Solution {
    int[][] directions = new int[][]{{0, -1}, {0, 1}, {-1, 0}, {1, 0}};
    int m;
    int n;

    public int islandPerimeter(int[][] grid) {
        m = grid.length;
        n = grid[0].length;
        int result = 0;
        for(int i = 0;i < m;i++){
            for(int j = 0;j < n;j++){
                if(grid[i][j] == 1){
                    result += dfs(grid, i, j);
                }
            }
        }
        return result;
    }

    private int dfs(int[][] grid, int i, int j){
        if(i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == 0){
            return 1;
        }
        if(grid[i][j] == 2){
            return 0;
        }
        //防止重复遍历
        grid[i][j] = 2;
        int count = 0;
        for(int[] direction:directions){
            int x = i + direction[0];
            int y = j + direction[1];
            count += dfs(grid, x, y);
        }
        return count;
    }
}
```





