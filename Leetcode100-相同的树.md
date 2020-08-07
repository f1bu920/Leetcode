---
title: Leetcode100.相同的树
date: 2020-08-07 10:10:55
categories: Leetcode
tags:
  - 树
---

##  Leetcode100.相同的树

给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

[题目链接](https://leetcode-cn.com/problems/same-tree)

<!--more-->

示例 1:

    输入:       1         1
              / \       / \
             2   3     2   3
    		[1,2,3],   [1,2,3]
    输出: true


示例 2:

    输入:      1          1
              /           \
             2             2
    	    [1,2],     [1,null,2]
    输出: false


示例 3:

    输入:       1         1
              / \       / \
             2   1     1   2   
            [1,2,1],   [1,1,2]
    输出: false



### 思路

先判断这两个节点是否为空节点，再判断他们的值是否相等并递归调用判断左子节点和右子节点。



### 代码实现

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null&&q==null){
            return true;
        }
        if(p==null||q==null){
            return false;
        }
        return p.val==q.val&&isSameTree(p.left,q.left)&&isSameTree(p.right,q.right);
    }
}
```

