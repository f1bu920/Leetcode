---
title: Leetcode40.组合总和II
date: 2020-09-10 09:15:00
categories: Leetcode
tags:
  - 回溯
---

## Leetcode40.组合总和II

给定一个数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个数字在每个组合中只能使用一次。

[题目链接](https://leetcode-cn.com/problems/combination-sum-ii)

<!--more-->

说明：

所有数字（包括目标数）都是正整数。
解集不能包含重复的组合。 
示例 1:

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```



示例 2:

```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```



### 思路

因为不能有重复的集合，所以需要按顺序进行搜索并剪枝。



### 代码实现

```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    List<Integer> path = new ArrayList<>();

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        //先进行排序
        Arrays.sort(candidates);
        dfs(candidates, 0, target);
        return result;
    }

    private void dfs(int[] candidates, int index, int leftNum) {
        //添加到结果中
        if (leftNum == 0) {
            result.add(new ArrayList<>(path));
            return;
        }
        for (int i = index; i < candidates.length; i++) {
            //剪枝
            if (leftNum - candidates[i] < 0) {
                break;
            }
            //去重
            if (i > index && candidates[i] == candidates[i - 1]) {
                continue;
            }
            path.add(candidates[i]);
            dfs(candidates, i + 1, leftNum - candidates[i]);
            path.remove(path.size() - 1);
        }
    }
}
```

