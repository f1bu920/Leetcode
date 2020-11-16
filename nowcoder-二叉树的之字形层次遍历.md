---
title: nowcoder-二叉树的之字形层次遍历
date: 2020-11-16 14:17:46
category: Nowcoder
tags:
  - 树
  - 层次遍历
---

# nowcoder-二叉树的之字形层次遍历

## 题目描述

给定一个二叉树，返回该二叉树的之字形层序遍历，（第一层从左向右，下一层从右向左，一直这样交替）
例如：
给定的二叉树是{3,9,20,#,#,15,7},
![img](https://uploadfiles.nowcoder.com/images/20200807/999991351_1596788654427_630E55F47DBAFBF72C88E265929E43F7)
该二叉树之字形层序遍历的结果是

> [
>
> [3],
>
> [20,9],
>
> [15,7]
>
> ]

示例1

## 输入

```
{1,#,2}
```

## 返回值

```
[[1],[2]]
```



## 思路

使用队列存储每层的节点，另外使用一个变量`positive`判断这层是正向遍历还是逆向遍历。



## 代码实现

```java
public class Solution {
    /**
     * 
     * @param root TreeNode类 
     * @return int整型ArrayList<ArrayList<>>
     */
    public ArrayList<ArrayList<Integer>> zigzagLevelOrder (TreeNode root) {
        // write code here
        ArrayList<ArrayList<Integer>> result = new ArrayList();
        if (root == null) {
            return result;
        }
        LinkedList<TreeNode> queue = new LinkedList();
        queue.add(root);
        boolean positive = true;
        while (!queue.isEmpty()) {
            int size = queue.size();
            ArrayList<Integer> list = new ArrayList(size);
            //正向遍历
            if (positive) {
                for (int i = 0; i < size; i++) {
                    TreeNode node = queue.poll();
                    list.add(node.val);
                    if (node.left != null) {
                        queue.add(node.left);
                    }
                    if (node.right != null) {
                        queue.add(node.right);
                    }
                }
                //逆向遍历
            } else {
                for (int i = size - 1; i >= 0; i--) {
                    TreeNode node = queue.pollLast();
                    list.add(node.val);
                    if (node.right != null) {
                        //将节点添加到队列的头部
                        queue.addFirst(node.right);
                    }
                    if (node.left != null) {
                        queue.addFirst(node.left);
                    }
                }

            }
            positive = !positive;
            result.add(list);
        }
        return result;
    }
}
```

