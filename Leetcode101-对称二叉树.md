---
title: Leetcode101.对称二叉树
date: 2020-05-31 09:23:56
categories: Leetcode
tags:
  - 树
  - 递归
  - 层序遍历
---

## Leetcode101.对称二叉树

给定一个二叉树，检查它是否是镜像对称的。

 [题目链接](https://leetcode-cn.com/problems/symmetric-tree)

<!--more-->

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

        1
       / \
      2   2
     / \ / \
    3  4 4  3



但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    	1
       / \
      2   2
       \   \
       3    3



进阶：

你可以运用递归和迭代两种方法解决这个问题吗？

#### 思路

递归，判断一颗二叉树是否对称，就是判断左子树和右子树是否镜像对称。镜像对称有两个条件：

- 根节点值相等
- 每个树的左子树和右子树都对称。

令两个指针`p`、`q`分别指向根节点，通过同步移动这两个指针来遍历这颗树，`p`左移时`q`右移，`p`右移时`q`左移，每次检查`p`和`q`对应的值是否相等。



迭代方式可以建立辅助队列来进行层序遍历。

#### 代码实现

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return check(root, root);
    }

    private boolean check(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }
        if (p == null || q == null) {
            return false;
        }
        return p.val == q.val && check(p.left, q.right) && check(p.right, q.left);
    }
}
```



