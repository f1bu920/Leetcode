---
title: Leetcode841.钥匙和房间
date: 2020-08-31 15:04:48
categories: Leetcode
tags:
  - 深度优先搜素
---

## Leetcode841.钥匙和房间

有 `N` 个房间，开始时你位于 0 号房间。每个房间有不同的号码：`0，1，2，...，N-1`，并且房间里可能有一些钥匙能使你进入下一个房间。

在形式上，对于每个房间 `i` 都有一个钥匙列表 `rooms[i]`，每个钥匙 `rooms[i][j]` 由 [0,1，...，N-1] 中的一个整数表示，其中 `N = rooms.length`。 钥匙 `rooms[i][j] = v` 可以打开编号为 `v` 的房间。

最初，除 0 号房间外的其余所有房间都被锁住。

你可以自由地在房间之间来回走动。

如果能进入每个房间返回 true，否则返回 false。

[题目链接](https://leetcode-cn.com/problems/keys-and-rooms)

<!--more-->

示例 1：

```
输入: [[1],[2],[3],[]]
输出: true
解释:  
我们从 0 号房间开始，拿到钥匙 1。
之后我们去 1 号房间，拿到钥匙 2。
然后我们去 2 号房间，拿到钥匙 3。
最后我们去了 3 号房间。
由于我们能够进入每个房间，我们返回 true。
```



示例 2：

```
输入：[[1,3],[3,0,1],[2],[0]]
输出：false
解释：我们不能进入 2 号房间。
提示：

1 <= rooms.length <= 1000
0 <= rooms[i].length <= 1000
所有房间中的钥匙数量总计不超过 3000。
```



### 思路

创建一个访问数组`visited[n]`，使用`num`统计访问过的房间数，当将要访问的房间已被访问过，则跳过。最后返回`num==n`。



### 代码实现

```java
class Solution {
    //访问数组，默认为false
    boolean[] visited;
    //访问过的房间数
    int num;

    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        int n = rooms.size();
        num = 0;
        visited = new boolean[n];
        dfs(rooms, 0);
        return num == n;
    }

    private void dfs(List<List<Integer>> rooms, int x) {
        visited[x] = true;
        num++;
        for (int key : rooms.get(x)) {
            //如果房间没访问过，则进行dfs递归
            if (!visited[key]) {
                dfs(rooms, key);
            }
        }
    } 
}
```

