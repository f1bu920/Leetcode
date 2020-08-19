---
title: Leetcode109.有序链表转换二叉搜索树
date: 2020-08-18 15:41:55
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode109.有序链表转换二叉搜索树

给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

[题目链接](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree)

<!--more-->

示例:

给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      	   0
     	  / \
        -3   9
       /   /
     -10  5


### 思路

先遍历链表，将链表元素添加到`list`中。因为要构造二叉搜索树，所以使用二分法，每次选择中间元素，构造成树节点，再递归地将左右子节点链接到这个树节点上。



### 代码实现

```java
class Solution {
    List<ListNode> list = new ArrayList();
    public TreeNode sortedListToBST(ListNode head) {
        ListNode cur = head;
        while(cur!=null){
            list.add(cur);
            cur = cur.next;
        }
        return buildBST(0,list.size()-1);
    }
    private TreeNode buildBST(int left,int right){
        if(left>right){
            return null;
        }
        int mid = left+(right-left)/2;
        TreeNode root = new TreeNode(list.get(mid).val);
        root.left = buildBST(left,mid-1);
        root.right = buildBST(mid+1,right);
        return root;
    }
}
```

