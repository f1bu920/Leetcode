---
title: Leetcode106.从中序与后序遍历序列构造二叉树
date: 2020-09-25 10:43:32
categories: Leetcode
tags:
  - 树
  - 递归
---

##  Leetcode106.从中序与后序遍历序列构造二叉树

根据一棵树的中序遍历与后序遍历构造二叉树。

[题目链接](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal)

<!--more-->

注意:
你可以假设树中没有重复的元素。

例如，给出

```
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
```



返回如下的二叉树：

    	3
       / \
      9  20
        /  \
       15   7


### 思路

中序遍历的顺序是左孩子->根节点->右孩子；

后序遍历的顺序是左孩子->右孩子->根节点。

所以**后续遍历序列的最后一个元素代表根节点，所以可以建立中序序列的哈希表来实现`O(1)`复杂度查找根节点在中序遍历序列中的下标。**然后将中序序列分为两部分，左边部分为左子树，右边部分为右子树，继续递归。



### 代码实现

```java
class Solution {
    //存储中序序列中元素与下标的对应关系
    Map<Integer,Integer> map;
    int[] inorder;
    int[] postorder;
    //指向后序遍历序列的最后一个元素
    int postIndex;
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        this.inorder = inorder;
        this.postorder = postorder;
        this.postIndex = postorder.length-1;
        this.map = new HashMap(postorder.length);
        for(int i = 0;i<inorder.length;i++){
            map.put(inorder[i],i);
        }
        return buildTree(0,postIndex);
    }
    
    private TreeNode buildTree(int left,int right){
        if(left>right){
            return null;
        }
        int val = postorder[postIndex];
        postIndex--;
        int index = map.get(val);
        TreeNode root = new TreeNode(val);
        root.right = buildTree(index+1,right);
        root.left = buildTree(left,index-1);
        return root;
    }
}
```

