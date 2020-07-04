---
title: Leetcode39.组合总和
date: 2020-07-04 08:47:40
categories: Leetcode
tags:
  - 回溯
---

## Leetcode39.组合总和

给定一个无重复元素的数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 

[题目链接](https://leetcode-cn.com/problems/combination-sum)

<!--more-->

示例 1:

```
输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
```



示例 2:

```
输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```



### 思路

[参考链接](https://leetcode-cn.com/problems/combination-sum/solution/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-m-2/)

回溯思想，将数组排序，每次减去数组中`begin`指向的数字，直到剩余数值`leftNum`为0，将当前序列添加到结果中。从`begin`起遍历整个数组，直到`leftNum<candidates[i]`，因为数组有序，所以剩下的数字可以全部剪枝。



### 代码实现

```java
class Solution {
    //全局结果
    List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        //将数组排序
        Arrays.sort(candidates);
        dfs(candidates, target, 0, target, new ArrayList<>());
        return result;
    }
    //begin是本轮搜索起点下标，设置begin是为了去重复，因为一个节点可以使用多次，所以下轮搜索从当前起点开始
    //leftNum是剩余数值
    //path是从根节点到任意节点的路径
    private void dfs(int[] candidates, int target, int begin, int leftNum, ArrayList<Integer> path) {
        if (leftNum == 0) {
            //leftNum为0，将当前路径添加到结果中
            //因为path只有一份，所以需要做一个拷贝
            result.add(new ArrayList<>(path));
            return;
        }
        for (int i = begin; i < candidates.length; i++) {
            //在数组有序情况下进行剪枝
            if (leftNum - candidates[i] < 0) {
                break;
            }
            path.add(candidates[i]);
            dfs(candidates, target, i, leftNum - candidates[i], path);
            path.remove(path.size() - 1);
        }
    }
}
```



