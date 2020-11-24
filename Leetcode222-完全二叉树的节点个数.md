---
title: Leetcode222.完全二叉树的节点个数
date: 2020-11-24 12:47:19
category: Leetcode
tags:
  - 树
  - 二分搜索
---

## Leetcode222.完全二叉树的节点个数

给出一个完全二叉树，求出该树的节点个数。

说明：

完全二叉树的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。

[题目链接](https://leetcode-cn.com/problems/count-complete-tree-nodes)

<!--more-->

示例:

```
输入: 
    1
   / \
  2   3
 / \  /
4  5 6

输出: 6
```



### 思路

对于一颗完全二叉树，层数为h，则总结点数为`2^h - 1 `。对`root`节点的左右子树进行高度统计，`left`为左子树高度，`right`为右子树高度，如果`left==right`，则代表叶子节点层左子树完全排满，是完全二叉树，将结果加上`1<<left`，同时将`root`更新到右子节点；如果`left != right`，则代表叶子结点层左子树未排满，可知右子树的最后一层是完全二叉树且高度为`right`，所以结果加上`1<<right`，更新`root`为左子节点。



### 代码实现

```java
class Solution {
    public int countNodes(TreeNode root) {
        if(root == null){
            return 0;
        }
        int count = 0;
        //左子树的层数
        int left = TreeLevel(root.left);
        while(root != null){
            //右子树的层数
            int right = TreeLevel(root.right);
            //层数相等，代表左子树是完全二叉树
            if(left == right){
                //添加到结果中
                count += (1<<left);
                root = root.right;
                //不相等，代表左子树不是完全二叉树，但右子树是完全二叉树
            }else{
                count += (1<<right);
                root = root.left;
            }
            //开始遍历下一层，将左子树层数减一
            left--;
        }
        return count;
    }

    private int TreeLevel(TreeNode root){
        if(root == null){
            return 0;
        }
        return 1 + TreeLevel(root.left);
    }
}
```

