---
title: Leetcode78.子集
date: 2020-07-15 11:56:21
categories: Leetcode
tags:
  - 回溯
---

## Leetcode78.子集

给定一组不含重复元素的整数数组 `nums`，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

[题目链接](https://leetcode-cn.com/problems/subsets)

<!--more-->

示例:

```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```



### 思路

设置一个全局变量`result`来存储结果，创建一个中间变量`path`来记录回溯路径。

为了防止出现重复，设置一个下标`index`记录遍历到的位置。当`index>=nums.length`时结束；否则循环遍历。

### 代码实现

```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> path = new ArrayList<>();
        result.add(path);
        subsets(new ArrayList<Integer>(), nums, 0);
        return result;
    }

    private void subsets(List<Integer> path, int[] nums, int index) {
        //当到达最后一位时结束
        if (index == nums.length) {
            return;
        }
        for (int i = index; i < nums.length; i++) {
            //将当前元素添加到
            path.add(nums[i]);
            //将当前路径添加到结果中
            result.add(new ArrayList<>(path));
            subsets(path, nums, i + 1);
            //回退
            path.remove(path.size() - 1);
        }
    }
}
```





