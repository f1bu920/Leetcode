---
title: Leetcode501.二叉搜索树中的众数
date: 2020-09-24 09:25:07
categories: Leetcode
tags:
  - 树
---

##  Leetcode501.二叉搜索树中的众数

给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

结点左子树中所含结点的值小于等于当前结点的值
结点右子树中所含结点的值大于等于当前结点的值
左子树和右子树都是二叉搜索树

[题目链接](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree)

<!--more-->

例如：

```
给定 BST [1,null,2,2],

   1
    \
     2
    /
   2
返回[2].
```

提示：如果众数超过1个，不需考虑输出顺序

进阶：你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）



### 思路

维护三个变量`current`、`count`、`maxCount`分别记录上次遍历元素及其出现次数和最大出现次数。因为是二叉搜索树，所以中序遍历得到的是一个非递减的序列。

当当前值等于`current`时，`count`加一，如果等于`maxCount`，则将当前结果加入到`list`中，如果大于`maxCount`则将`list`清空后，将当前值加入`list`；如果当前值不等于`current`，则更新`current`和`count`。



### 代码实现

```java
class Solution {
    List<Integer> list = new ArrayList();
    int current = Integer.MIN_VALUE;
    int count = 0;
    int maxCount = 0;
    public int[] findMode(TreeNode root) {
        dfs(root);
        int[] result = new int[list.size()];
        int j = 0;
        for(int i:list){
            result[j++] = i;
        }
        return result;
    }
    private void dfs(TreeNode root){
        if(root==null){
            return ;
        }
        dfs(root.left);
        if(root.val!=current){
            current = root.val;
            count=1;
        }
        if(root.val==current){
            count++;
        }
        if(count==maxCount){
            list.add(root.val);
        }
        if(count>maxCount){
            maxCount = count;
            list.clear();
            list.add(root.val);
        }
        dfs(root.right);
    }
}
```

