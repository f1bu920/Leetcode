---
title: Leetcode538.把二叉搜索树转换为累加树
date: 2020-07-16 09:53:13
categories: Leetcode
tags:
  - 树
  - 中序遍历
  - 递归
---

## Leetcode538.把二叉搜索树转换为累加树

给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)，使得每个节点的值是原来的节点值加上所有大于它的节点值之和。

 [题目链接](https://leetcode-cn.com/problems/convert-bst-to-greater-tree)

<!--more-->

例如：

```
输入: 原始二叉搜索树:
              5
            /   \
           2     13

输出: 转换为累加树:
             18
            /   \
          20     13
```



### 思路

因为原始树是二叉搜索树，所以逆序的中序遍历得到的就是递减的顺序，即中序遍历先遍历右子树再遍历左子树。设置一个全局变量`sum`保存遍历总和。



### 代码实现

```java
class Solution {
    //sum保存比当前节点大的节点之和
    int sum = 0;

    public TreeNode convertBST(TreeNode root) {
        if (root == null) {
            return root;
        }
        midOrder(root);
        return root;
    }

    private void midOrder(TreeNode root) {
        if (root == null) {
            return;
        }
        //先遍历右子树
        midOrder(root.right);
        //更新节点值
        root.val += sum;
        //更新sum值
        sum = root.val;
        midOrder(root.left);
    }
}
```



也可以利用栈将上面递归形式改为迭代形式。