---
title: Leetcode102.二叉树的层序遍历
date: 2020-05-13 08:58:21
tags:
  - 树
  - 层序遍历
  - 队列
---

## Leetcode102.二叉树的层序遍历

给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

 [题目链接](https://leetcode-cn.com/problems/binary-tree-level-order-traversal)

<!--more-->

示例：

```
二叉树：[3,9,20,null,null,15,7],

    3

   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]
```

#### 思路

借助辅助队列，进行二叉树的层序遍历，对于每一层，设置一个变量`size`记录这一层的元素个数，将这一层的元素全部出队。



#### 代码实现

```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> levelOrder(TreeNode root) {
        if (root == null) {
            return result;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            List<Integer> list = new ArrayList<>();
            int size = queue.size();
            //将这一层的元素全部出队
            for (int i = 0; i < size; i++) {
                TreeNode poll = queue.poll();
                list.add(poll.val);
                if (poll.left != null) {
                    queue.add(poll.left);
                }
                if (poll.right != null) {
                    queue.add(poll.right);
                }
            }
            result.add(list);
        }
        return result;
    }
}
```



