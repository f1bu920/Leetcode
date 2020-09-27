---
title: Leetcode235.二叉搜索树的最近公共祖先
date: 2020-09-27 18:54:29
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode235.二叉搜索树的最近公共祖先

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]

![](https://f1bu920.github.io/images/Leetcode235二叉搜索树的最近公共祖先.png)

 [题目链接](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree)

<!--more-->

示例 1:

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```



示例 2:

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
```




说明:

所有节点的值都是唯一的。
p、q 为不同节点且均存在于给定的二叉搜索树中。



### 思路

因为是二叉搜索树，所以每次先判断当前节点`root`的值是否都大于`p`、`q`，如果是则最近公共祖先在左子树中；

判断`root`的值是否都小于`p`、`q`，如果是则最近公共祖先在右子树中；否则最近公共祖先就是`root`。



### 代码实现

- 递归

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val<p.val&&root.val<q.val){
            return lowestCommonAncestor(root.right,p,q);
        }
        if(root.val>p.val&&root.val>q.val){
            return lowestCommonAncestor(root.left,p,q);
        }
        return root;
    }
}
```

- 一次遍历

```java

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode cur = root;
        while(true){
            if(cur.val<p.val&&cur.val<q.val){
                cur = cur.right;
            }
            else if(cur.val>p.val&&cur.val>q.val){
                cur = cur.left;
            }else{
                return cur;
            }
        }
    }
}
```



