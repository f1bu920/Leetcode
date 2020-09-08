---
title: Leetcode77.组合
date: 2020-09-08 08:45:35
categories: Leetcode
tags:
  - 回溯
---

## Leetcode77.组合

给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

[题目链接](https://leetcode-cn.com/problems/combinations)

<!--more-->

示例:

```
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```



### 思路

利用回溯进行dfs。



### 代码实现

```java
class Solution {
    int n;
    int k;

    public List<List<Integer>> combine(int n, int k) {
        this.n = n;
        this.k = k;
        List<List<Integer>> result = new ArrayList();
        List<Integer> path = new ArrayList<>();
        dfs(result, path, 1);
        return result;
    }

    private void dfs(List<List<Integer>> result, List<Integer> path, int index) {
        if (path.size() == k) {
            //注意这里要new ArrayList<>(path)
            result.add(new ArrayList<>(path));
            return;
        }
        //进行剪枝，k-path.size()指的是还需要添加几个元素
        //当n小于等于n - (k - path.size()) + 1时，必定无法构成一个组合，直接剪枝
        for (int i = index; i <= n - (k - path.size()) + 1; i++) {
            path.add(i);
            dfs(result, path, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```

