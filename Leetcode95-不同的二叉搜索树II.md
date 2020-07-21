---
title: Leetcode95.不同的二叉搜索树II
date: 2020-07-21 09:19:48
categories: Leetcode
tags:
  - 递归
  - 树
---

## Leetcode95.不同的二叉搜索树II

给定一个整数 `n`，生成所有由 1 ... n 为节点所组成的 二叉搜索树 。

 [题目链接](https://leetcode-cn.com/problems/unique-binary-search-trees-ii)

<!--more-->

示例：

```
输入：3
输出：
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释：
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```




提示：

- 0 <= n <= 8



### 思路

[官方题解](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/solution/bu-tong-de-er-cha-sou-suo-shu-ii-by-leetcode-solut/)

枚举根节点值`i`，因为是二叉搜索树，所以左子树序列为`[1...i-1]`，右子树序列为`[i+1...n]`。接着递归枚举左子树序列和右子树序列。

定义递归函数`generateTrees(int start, int end)`，当`start>end`时，没有数字，将`null`加入结果中。当`start==end`时，只有一个数字，将这个数字构造成一棵树加入结果中。枚举每个数字作为根节点，递归得到所有的左子树和所有的右子树，将根节点与左子树集合和右子树集合结合，并将根节点添加到结果中。



### 代码实现

```java
class Solution {
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) {
            return new ArrayList<>();
        }
        return generateTrees(1, n);
    }

    private List<TreeNode> generateTrees(int start, int end) {
        List<TreeNode> result = new ArrayList<>();
        //将null添加到结果中
        if (start > end) {
            result.add(null);
            return result;
        }
        //只有一个数字
        if (start == end) {
            result.add(new TreeNode(start));
            return result;
        }
        //枚举每个数字作为根节点
        for (int i = start; i <= end; i++) {
            //得到所有的左子树
            List<TreeNode> lefts = generateTrees(start, i - 1);
            //得到所有的右子树
            List<TreeNode> rights = generateTrees(i + 1, end);
            //左子树与右子树两两结合
            for (TreeNode left : lefts) {
                for (TreeNode right : rights) {
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    result.add(root);
                }
            }
        }
        return result;
    }
}
```

