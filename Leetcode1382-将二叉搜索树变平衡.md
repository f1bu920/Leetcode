---
title: Leetcode1382.将二叉搜索树变平衡
date: 2020-07-17 10:06:14
categories: Leetcode
tags:
  - 树
  - 中序遍历
---

##  Leetcode1382.将二叉搜索树变平衡

给你一棵二叉搜索树，请你返回一棵 平衡后 的二叉搜索树，新生成的树应该与原来的树有着相同的节点值。

如果一棵二叉搜索树中，每个节点的两棵子树高度差不超过 1 ，我们就称这棵二叉搜索树是 平衡的 。

如果有多种构造方法，请你返回任意一种。

 [题目链接](https://leetcode-cn.com/problems/balance-a-binary-search-tree)

<!--more-->

示例：

```
输入：root = [1,null,2,null,3,null,4,null,null]
输出：[2,1,3,null,null,null,4]
解释：这不是唯一的正确答案，[3,1,4,null,2,null,null] 也是一个可行的构造方案。
```




提示：

- 树节点的数目在 1 到 10^4 之间。
- 树节点的值互不相同，且在 1 到 10^5 之间。



### 思路

利用中序遍历构造出升序序列，然后与[Leetcode108.将有序数组转化为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)相同，利用二分法构造平衡二叉搜索树。



### 代码实现

```java
class Solution {
    List<TreeNode> list = new ArrayList<>();
    public TreeNode balanceBST(TreeNode root) {
        preOrder(root);
        int size = list.size();
        return convertListToBST(0,size-1);
    }
    //中序遍历构造升序序列
    private void preOrder(TreeNode root){
        if(root == null){
            return;
        }
        preOrder(root.left);
        list.add(root);
        preOrder(root.right);
    }
    //将升序序列转化为BST
    private TreeNode convertListToBST(int left, int right){
        if(left>right){
            return null;
        }
        int mid = left+(right-left)/2;
        TreeNode root = list.get(mid);
        root.left = convertListToBST(left,mid-1);
        root.right = convertListToBST(mid+1,right);
        return root;
    }
}
```



