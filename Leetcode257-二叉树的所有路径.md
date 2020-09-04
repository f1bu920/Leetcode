---
title: Leetcode257.二叉树的所有路径
date: 2020-09-04 11:44:00
categories: Leetcode
tags:
  - 深度优先搜索
  - 回溯
---

##  Leetcode257.二叉树的所有路径

给定一个二叉树，返回所有从根节点到叶子节点的路径。

说明: 叶子节点是指没有子节点的节点。

[题目链接](https://leetcode-cn.com/problems/binary-tree-paths)

<!--more-->

示例:

```
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```



### 思路

先判断当前节点是否是叶子节点，如果是，则将当前列表添加到结果中。如果不是则进行深度优先搜素。

使用`list`来存储当前路径上的节点，定义一个方法将其转化为`String`格式。



### 代码实现

```java
class Solution {
    List<String> result = new ArrayList();

    public List<String> binaryTreePaths(TreeNode root) {
        if (root == null) {
            return result;
        }
        binaryTreePathsSearch(root, new ArrayList<>());
        return result;
    }
    //dfs+回溯
    private void binaryTreePathsSearch(TreeNode root, List<Integer> list) {
        list.add(root.val);
        //如果是叶子节点，将当前路径添加到结果中
        if (root.left == null && root.right == null) {
            result.add(convertListToString(list));
        }
        //进行dfs
        if (root.left != null) {
            binaryTreePathsSearch(root.left, list);
        }
        if (root.right != null) {
            binaryTreePathsSearch(root.right, list);
        }
        //一定记得回溯
        list.remove(list.size() - 1);
    }
    //将路径列表转化为String格式
    private String convertListToString(List<Integer> list) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < list.size() - 1; i++) {
            sb.append(list.get(i)).append("->");
        }
        sb.append(list.get(list.size() - 1));
        return sb.toString();
    }
}
```

