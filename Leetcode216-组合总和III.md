---
title: Leetcode216.组合总和III
date: 2020-09-11 16:06:14
categories: Leetcode
tags:
  - 回溯
---

## Leetcode216.组合总和III

找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

说明：

所有数字都是正整数。
解集不能包含重复的组合。 

[题目链接](https://leetcode-cn.com/problems/combination-sum-iii)

<!--more-->

示例 1:

```
输入: k = 3, n = 7
输出: [[1,2,4]]
```



示例 2:

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
```



### 思路

因为只允许用`[1-9]`的数字，所以枚举时从1开始，到9为止。因为每种组合中都不包含重复的数字，所以需要使用`index`来记录遍历过的下标。因为不能包含重复的组合，所以递归时要`i+1`。



### 代码实现

```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    List<Integer> path = new ArrayList<>();

    public List<List<Integer>> combinationSum3(int k, int n) {
        dfs(k, n, 1);
        return result;
    }

    private void dfs(int k, int n, int index) {
        //同时满足这两个条件才是结果
        if (k == 0 && n == 0) {
            result.add(new ArrayList<>(path));
            return;
        }
        for (int i = index; i <= 9; i++) {
            //剪枝
            if (n - i < 0) {
                break;
            }
            //剪枝
            if (k <= 0) {
                return;
            }
            path.add(i);
            dfs(k - 1, n - i, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```



