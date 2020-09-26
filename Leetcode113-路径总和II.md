---
title: Leetcode113.路径总和II
date: 2020-09-26 09:39:03
categories: Leetcode
tags:
  - 树
  - 回溯
---

## Leetcode113.路径总和II

给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

[题目链接](https://leetcode-cn.com/problems/path-sum-ii)

<!--more-->

示例:
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```



### 思路

深度优先遍历，利用回溯思想，枚举每一条从根节点到叶子结点的路径，当遍历到叶子节点且此时路径和等于目标时，就找到了一条路径。



### 代码实现

```java
class Solution {
    List<List<Integer>> result = new ArrayList();
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        if(root==null){
            return result;
        }
        dfs(root,new ArrayList<Integer>(),sum);
        return result;
    }
    private void dfs(TreeNode root,List<Integer> path,int sum){
        if(root==null){
            return;
        }
        sum-=root.val;
        path.add(root.val);
        if(sum==0&&root.left==null&&root.right==null){
            result.add(new ArrayList(path));
        }
        dfs(root.left,path,sum);

        dfs(root.right,path,sum);
        path.remove(path.size()-1);
    }
}
```

