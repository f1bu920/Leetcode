---
title: Leetcode105.从前序与中序遍历序列构造二叉树
date: 2020-05-22 12:37:52
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode105.从前序与中序遍历序列构造二叉树

根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

[题目链接](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)

<!--more-->

例如，给出

前序遍历 `preorder` = [3,9,20,15,7]
中序遍历 `inorder` = [9,3,15,20,7]
返回如下的二叉树：

        3
       / \
      9  20
        /  \
       15   7
#### 思路

[参考链接](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/solution/cong-qian-xu-yu-zhong-xu-bian-li-xu-lie-gou-zao-9/)

对于任意一颗二叉树，前序遍历的结果总是：根节点-->左子树的前序遍历结果-->右子树的前序遍历结果。即根节点总是前序遍历的第一个节点。

中序遍历的结果总是：左子树的中序遍历结果-->根节点-->右子树的中序遍历结果。

所以，我们可以在中序遍历中定位到根节点所在的位置，然后我们就可以知道左子树和右子树的节点数目。对于同一棵树，左子树和右子树的长度相同，所以我们又知道了左子树和右子树的前序和中序遍历结果。我们就可以递归地构造出左子树和右子树，并连接到根节点上。

我们在中序遍历中定位根节点位置时需要从头到尾遍历，会增加复杂度。题中说明了树中没有重复的元素，所有可以建立哈希表存储树中元素与数组索引的对应关系。

![](https://f1bu920.github.io/images/Leetcode105-从前序与中序遍历序列构造二叉树.png)

#### 代码实现

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int len = preorder.length;
        //哈希表存储树中元素与中序遍历下标的对应关系
        Map<Integer, Integer> map = new HashMap<>(len);
        for (int i = 0; i < len; i++) {
            map.put(inorder[i], i);
        }
        //方法重载，构造根节点并将根节点的左右子树连接到根节点上
        return buildTree(preorder, map, 0, len - 1, 0, len - 1);
    }

    //preOrder: 前序遍历序列
    //preLeft：前序遍历序列子区间的左边界
    //preRight：前序遍历序列子区间的右边界
    //map：中序遍历中数值与下标的对应关系
    //inLeft：中序遍历序列子区间的左边界
    //inRight：中序遍历序列子区间的右边界
    private TreeNode buildTree(int[] preOrder, Map<Integer, Integer> map, int preLeft, int preRight, int inLeft, int inRight) {
        //递归终止条件为：不构成左闭右闭区间
        if (preLeft > preRight || inLeft > inRight) {
            return null;
        }
        //根节点值
        int rootVal = preOrder[preLeft];
        //根节点在中序遍历中的下标
        int pIndex = map.get(rootVal);
        TreeNode root = new TreeNode(rootVal);
        root.left = buildTree(preOrder, map, preLeft + 1, pIndex - inLeft + preLeft, inLeft, pIndex - 1);
        root.right = buildTree(preOrder, map, pIndex - inLeft + preLeft + 1, preRight, pIndex + 1, inRight);
        return root;
    }
}
```



