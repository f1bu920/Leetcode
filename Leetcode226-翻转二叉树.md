---
title: Leetcode226.翻转二叉树
date: 2020-06-19 14:19:13
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode226.翻转二叉树

翻转一棵二叉树。

[题目链接](https://leetcode-cn.com/problems/invert-binary-tree)

<!--more-->

示例：

输入：

          4
        /   \
      2     7
     / \   / \
    1   3 6   9

输出：

          4
        /   \
      7     2
     / \   / \
    9   6 3   1

### 思路

- 递归

  翻转二叉树需要将一个节点下的左右两个子节点更换位置，很明显具有递归结构。

- 迭代

  翻转二叉树需要交换树中所有结点的左右子节点，可以利用队列。

  创建一个队列，初始时将根节点添加进队列，每次出队时更换出队节点的左右子节点，并将非空左右子节点入队。最后返回根节点。



### 代码实现

- 递归

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root==null){
            return null;
        }
        TreeNode left = invertTree(root.left);
        TreeNode right = invertTree(root.right);
        //更换左右子节点
        root.left = right;
        root.right = left;
        return root;
    }
}
```

- 迭代

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            TreeNode treeNode = queue.removeFirst();
            //交换左右子节点
            TreeNode temp = treeNode.left;
            treeNode.left = treeNode.right;
            treeNode.right = temp;
            //将左右子节点入队
            if (treeNode.left != null)
                queue.addLast(treeNode.left);
            if (treeNode.right != null)
                queue.addLast(treeNode.right);
        }
        return root;
    }
}
```



