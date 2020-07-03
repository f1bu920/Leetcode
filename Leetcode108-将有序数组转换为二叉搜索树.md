---
title: Leetcode108.将有序数组转换为二叉搜索树
date: 2020-07-03 09:09:46
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode108.将有序数组转换为二叉搜索树

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

[题目链接](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree)

<!--more-->

示例:

     给定有序数组: [-10,-3,0,5,9],
    
    一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：
    	   0
    	  / \
        -3   9
       /   /
     -10  5


### 思路

给定的排序序列可以看成是二叉搜索树的中序遍历序列。每次选择中间数字作为二叉树的根节点，这样左右子树的个数只会相差1以内。如果数组长度是奇数，则根节点唯一；如果为偶数，则可以选择中间位置左边的数字作为根节点。



### 代码实现

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        TreeNode root = sortedArrayToBST(nums,0,nums.length-1);
        return root;
    }
    private TreeNode sortedArrayToBST(int[] nums, int left, int right){
        if(left>right){
            return null;
        }
        int mid = left+(right-left)/2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = sortedArrayToBST(nums,left,mid-1);
        root.right = sortedArrayToBST(nums,mid+1,right);
        return root;
    }
}
```

