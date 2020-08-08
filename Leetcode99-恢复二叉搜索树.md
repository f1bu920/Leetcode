---
title: Leetcode99.恢复二叉搜索树
date: 2020-08-08 08:54:20
categories: Leetcode
tags:
  - 树
  - 递归
  - 中序遍历
---

## Leetcode99.恢复二叉搜索树

二叉搜索树中的两个节点被错误地交换。

请在不改变其结构的情况下，恢复这棵树。

[题目链接](https://leetcode-cn.com/problems/recover-binary-search-tree)

<!--more-->

示例 1:

```
输入: [1,3,null,null,2]

   1
  /
 3
  \
   2

输出: [3,1,null,null,2]

   3
  /
 1
  \
   2
示例 2:

输入: [3,1,4,null,null,2]

  3
 / \
1   4
   /
  2

输出: [2,1,4,null,null,3]

  2
 / \
1   4
   /
  3
```



进阶:

使用 O(n) 空间复杂度的解法很容易实现。
你能想出一个只使用常数空间的解决方案吗？



### 思路

先中序遍历二叉搜索树得到一个序列，然后两次遍历这个序列，找到两个逆序点，记录节点值。再次遍历二叉树，当遇到这两个节点值时，进行交换。

因为二叉搜索树中序遍历得到的是一个递增序列，有两个节点被错误交换，当这两个点相邻时，有一个逆序对；不相邻时，有两个逆序对。所以采用先从前往后遍历找到第一个点，再从后往前找到第二个点。

### 代码实现

```java
class Solution {
    //记录中序遍历结果
    List<Integer> list = new ArrayList<>();

    public void recoverTree(TreeNode root) {
        if (root == null) {
            return;
        }
        //中序遍历
        inOrder(root);
        //记录节点值
        int x = -1;
        int y = -1;
        //先从前往后找到第一个
        for (int i = 0; i < list.size() - 1; i++) {
            if (list.get(i) > list.get(i + 1)) {
                x = list.get(i);
                break;
            }
        }
        //再从后往前找到第二个
        for (int i = list.size() - 1; i > 0; i--) {
            if (list.get(i) < list.get(i - 1)) {
                y = list.get(i);
                break;
            }
        }
        //再次遍历树，交换节点
        swapTreeNode(root, 2, x, y);
    }

    private void inOrder(TreeNode root) {
        if (root == null) {
            return;
        }
        inOrder(root.left);
        list.add(root.val);
        inOrder(root.right);
    }
    //count代表更改的次数，当改了两次后，直接返回
    private void swapTreeNode(TreeNode root, int count, int x, int y) {
        if (root == null) {
            return;
        }
        //更改节点的值
        if (root.val == x || root.val == y) {
            if (root.val == x) {
                root.val = y;
            } else {
                root.val = x;
            }
            if (--count <= 0) {
                return;
            }
        }
        swapTreeNode(root.left, count, x, y);
        swapTreeNode(root.right, count, x, y);
    }
}
```



