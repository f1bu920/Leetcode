---
title: Leetcode47.全排列II
date: 2020-09-18 09:40:04
categories: Leetcode
tags:
  - 回溯
---

## Leetcode47.全排列II

给定一个可包含重复数字的序列，返回所有不重复的全排列。

[题目链接](https://leetcode-cn.com/problems/permutations-ii)

<!--more-->

示例:

```
输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```



### 思路

此题在全排列的基础上添加了可包含重复数字的限制，所以结果中一定会产生重复。

在枚举之前先对数组进行排序，然后进行剪枝。剪枝的地方主要有两个：

- `used[i]`，当前元素使用过
- `nums[i]==nums[i-1]&&!used[i-1]`，当前元素已枚举过且当前元素刚刚被撤销。



### 代码实现

```java
class Solution {
    List<List<Integer>> result = new ArrayList();
    int n;
    boolean[] used;
    public List<List<Integer>> permuteUnique(int[] nums) {
        n = nums.length;
        used = new boolean[n];
        Arrays.sort(nums);
        dfs(nums,0,new ArrayList());
        return result;
    }
    private void dfs(int[] nums,int index,List<Integer> path){
        if(index==n){
            result.add(new ArrayList(path));
            return;
        }
        for(int i = 0;i<n;i++){
            if(used[i]){
                continue;
            }
            //进行剪枝  刚才已经枚举过，刚刚被撤销
            if(i!=0&&nums[i]==nums[i-1] && !used[i - 1]){
                continue;
            }
            path.add(nums[i]);
            used[i] = true;
            dfs(nums,index+1,path);
            used[i] = false;
            path.remove(path.size()-1);
        }
    }
}
```

