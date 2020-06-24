---
title: Leetcode236.二叉树的最近公共祖先
date: 2020-05-12 20:33:45
tags:
  - 递归
  - 树
---

##  Leetcode236.二叉树的最近公共祖先

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]

![Leetcode236二叉树的最近公共祖先binarytree.png](https://f1bu920.github.io/images/Leetcode236二叉树的最近公共祖先binarytree.png)

 [题目链接](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree)

<!--more-->

[参考链接](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/solution/236-er-cha-shu-de-zui-jin-gong-gong-zu-xian-hou-xu/)

示例 1:

输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
示例 2:

输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。


说明:

所有节点的值都是唯一的。
p、q 为不同节点且均存在于给定的二叉树中。



#### 思路

设`root`为节点`p`、`q`的某公共祖先，若其左子节点`root.left`和右子节点`root.right`都不是`p`、`q`的公共祖先，则称`root`为最近的公共祖先。

若`root`为`p`、`q`的公共祖先，则只能为以下情况：

1. `p`和`q`在`root`的子树中，且分列在`root`的两侧；
2. `p==root`，且`q`在左右子树中；
3. `q==root`，且`p`在左右子树中。

对二叉树进行后序遍历，当遇到`p`或`q`时返回；但`p`、`q`在节点`root`的两侧时，返回`root`。

- 终止条件

  当越过叶子节点，返回`null`。

  当`root==p||root==q`，返回`root`。

- 递归左子节点，返回值为`left`。

- 递归右子节点，返回值为`right`。

- 根据`left`和`right`，共有四种情况：

  1. `left`与`right`同时为空，`root`的左右子树中都不包含`p`、`q`，返回`null`。
  2. `left`和`right`同时不为空，`p`、`q`分布在两侧，返回`root`。
  3. `left`为空，`right`不为空，`p`、`q`都不在`root`的左子树中，直接返回`right`。
     1. `p`、`q`其中一个在`root`的右子树中。
     2. `p`、`q`都在`root`的右子树中，此时`right`指向最近的公共祖先节点。
  4. `left`不为空，`right`为空，与3同理。

![](https://f1bu920.github.io/images/Leetcode236.二叉树的最近公共祖先.png)



#### 代码实现

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left == null && right == null) {
            return null;
        }
        if (left == null) {
            return right;
        }
        if (right == null) {
            return left;
        }
        return root;    
    }
}
```



