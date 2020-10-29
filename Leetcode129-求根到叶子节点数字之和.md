---
title: Leetcode129.求根到叶子节点数字之和
date: 2020-10-29 09:51:37
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode129.求根到叶子节点数字之和

给定一个二叉树，它的每个结点都存放一个 0-9 的数字，每条从根到叶子节点的路径都代表一个数字。

例如，从根到叶子节点路径 1->2->3 代表数字 123。

计算从根到叶子节点生成的所有数字之和。

说明: 叶子节点是指没有子节点的节点。

[题目链接](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers)

<!--more-->

示例 1:

```
输入: [1,2,3]
    1
   / \
  2   3
输出: 25

解释:
从根到叶子节点路径 1->2 代表数字 12.
从根到叶子节点路径 1->3 代表数字 13.
因此，数字总和 = 12 + 13 = 25.
```


示例 2:

```
输入: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
输出: 1026

解释:
从根到叶子节点路径 4->9->5 代表数字 495.
从根到叶子节点路径 4->9->1 代表数字 491.
从根到叶子节点路径 4->0 代表数字 40.
因此，数字总和 = 495 + 491 + 40 = 1026.
```



### 思路

深度优先搜索，从根节点开始，遍历每个节点，如果是叶子节点，将叶子结点的值加到结果中；如果不是叶子节点，计算其对应的数字，进行递归遍历。



### 代码实现

```java
class Solution {
    public int sumNumbers(TreeNode root) {
        return sumNumbers(root, 0);
    }
    
    private int sumNumbers(TreeNode root, int preSum){
        if(root == null){
            return 0;
        }
        int sum = preSum * 10 + root.val;
        //叶子节点添加到结果中
        if(root.left == null && root.right == null){
            return sum;
        }else{
            //非叶子节点继续递归
            return sumNumbers(root.left, sum) + sumNumbers(root.right, sum);
        }
    }
}
```





