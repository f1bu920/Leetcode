---
title: Leetcode107.二叉树的层次遍历II
date: 2020-09-06 09:50:18
categories: Leetcode
tags:
  - 树
  - 广度优先遍历
---

## Leetcode107.二叉树的层次遍历II

给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

[题目链接](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii)

<!--more-->

例如：
给定二叉树 [3,9,20,null,null,15,7],

    	3
       / \
      9  20
        /  \
       15   7
    返回其自底向上的层次遍历为：
    
    [
      [15,7],
      [9,20],
      [3]
    ]


### 思路

和正常的层次遍历一样，只是将每层遍历结果添加进结果中使用头插法。



### 代码实现

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        LinkedList<List<Integer>> result = new LinkedList<>();
        bfs(root, result);
        return result;
    }

    private void bfs(TreeNode root, LinkedList<List<Integer>> result) {
        if (root == null) {
            return;
        }
        LinkedList<TreeNode> queue = new LinkedList();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.removeFirst();
                list.add(node.val);
                if (node.left != null) {
                    queue.addLast(node.left);
                }
                if (node.right != null) {
                    queue.addLast(node.right);
                }
            }
            //这里使用头插法
            result.addFirst(list);
        }
    }
}
```

