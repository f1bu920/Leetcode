---
title: Leetcode701.二叉搜索树中的插入操作
date: 2020-09-30 18:03:57
categories: Leetcode
tags:
  - 树
---

##  Leetcode701.二叉搜索树中的插入操作

给定二叉搜索树（BST）的根节点和要插入树中的值，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 输入数据保证，新值和原始二叉搜索树中的任意节点值都不同。

注意，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回任意有效的结果。

 [题目链接](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree)

<!--more-->

例如, 

给定二叉搜索树:

        4
       / \
      2   7
     / \
    1   3

和 插入的值: 5
你可以返回这个二叉搜索树:

         4
       /   \
      2     7
     / \   /
    1   3 5
或者这个树也是有效的:

         5
       /   \
      2     7
     / \   
    1   3
         \
          4


提示：

给定的树上的节点数介于 0 和 10^4 之间
每个节点都有一个唯一整数值，取值范围从 0 到 10^8
-10^8 <= val <= 10^8
新值和原始二叉搜索树中的任意节点值都不同



### 思路

因为是二叉搜索树，所以左子树一定小于根节点，右子树一定大于根节点。又因为确定要插入的值和元素二叉树中都不存在重复，所以可以先找到插入位置在进行插入。



### 代码实现

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if(root==null){
            return new TreeNode(val);
        }
        insert(root,val);
        return root;
    }
    private void insert(TreeNode root,int val){
        if(root.val>val&&root.left!=null){
            insert(root.left,val);
        }else if(root.val>val&&root.left==null){
            root.left = new TreeNode(val);
            return;
        }else if(root.val<val&&root.right!=null){
            insert(root.right,val);
        }else if(root.val<val){
            root.right = new TreeNode(val);
            return;
        }
    }
}
```



