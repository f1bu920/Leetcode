---
title: Leetcode174.地下城游戏
date: 2020-07-12 10:36:26
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode174.地下城游戏

一些恶魔抓住了公主（P）并将她关在了地下城的右下角。地下城是由 M x N 个房间组成的二维网格。我们英勇的骑士（K）最初被安置在左上角的房间里，他必须穿过地下城并通过对抗恶魔来拯救公主。

骑士的初始健康点数为一个正整数。如果他的健康点数在某一时刻降至 0 或以下，他会立即死亡。

有些房间由恶魔守卫，因此骑士在进入这些房间时会失去健康点数（若房间里的值为负整数，则表示骑士将损失健康点数）；其他房间要么是空的（房间里的值为 0），要么包含增加骑士健康点数的魔法球（若房间里的值为正整数，则表示骑士将增加健康点数）。

为了尽快到达公主，骑士决定每次只向右或向下移动一步。

编写一个函数来计算确保骑士能够拯救到公主所需的最低初始健康点数。

例如，考虑到如下布局的地下城，如果骑士遵循最佳路径 右 -> 右 -> 下 -> 下，则骑士的初始健康点数至少为 7。

-2 (K)	-3	3
-5	-10	1
10	30	-5 (P)

[题目链接](https://leetcode-cn.com/problems/dungeon-game)

<!--more-->


说明:

骑士的健康点数没有上限。

任何房间都可能对骑士的健康点数造成威胁，也可能增加骑士的健康点数，包括骑士进入的左上角房间以及公主被监禁的右下角房间。



### 思路

因为不知道初始时的健康点数，所以采用自顶向下的动态规划。令`dp[i][j]`代表到达`(i,j)`位置前所需的最少健康点数，`dungeon[i][j]`代表`(i,j)`处提供的健康点。到达当前位置`(i,j)`所需的最小健康点数等于下一个位置需要的最小健康点 减去 当前位置提供的健康点。即状态转移方程为`int temp = Math.min(dp[i + 1][j], dp[i][j + 1]) - dungeon[i][j]`， 当`temp<=0`时，即`(i,j)`位置提供的能量足够到达下一个位置，所以此时`dp[i][j] = 1`。

初始化：先计算最后一行和最后一列。



### 代码实现

```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        int m = dungeon.length;
        int n = dungeon[0].length;
        int[][] dp = new int[m][n];
        dp[m - 1][n - 1] = dungeon[m - 1][n - 1] >= 0 ? 1 : -dungeon[m - 1][n - 1] + 1;
        //最后一行
        for (int i = m - 2; i >= 0; i--) {
            int temp = dp[i + 1][n - 1] - dungeon[i][n - 1];
            dp[i][n - 1] = temp <= 0 ? 1 : temp;
        }
        //最后一列
        for (int i = n - 2; i >= 0; i--) {
            int temp = dp[m - 1][i + 1] - dungeon[m - 1][i];
            dp[m - 1][i] = temp <= 0 ? 1 : temp;
        }
        for (int i = m - 2; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {
                int temp = Math.min(dp[i + 1][j], dp[i][j + 1]) - dungeon[i][j];
                dp[i][j] = temp <= 0 ? 1 : temp;
            }
        }
        return dp[0][0];
    }
}
```

