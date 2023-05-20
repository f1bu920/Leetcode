---
title: 剑指offerII 115.重建序列
date: 2022-7-23 16:40:38
categories: nowcoder
tags:
  - 剑指offer
  - 拓扑排序
---

## 剑指offerII 115.重建序列

### 题目描述

给定一个长度为 n 的整数数组 nums ，其中 nums 是范围为 [1，n] 的整数的排列。还提供了一个 2D 整数数组 sequences ，其中 sequences[i] 是 nums 的子序列。
检查 nums 是否是唯一的最短 超序列 。最短 超序列 是 长度最短 的序列，并且所有序列 sequences[i] 都是它的子序列。对于给定的数组 sequences ，可能存在多个有效的 超序列 。

例如，对于 sequences = [[1,2],[1,3]] ，有两个最短的 超序列 ，[1,2,3] 和 [1,3,2] 。
而对于 sequences = [[1,2],[1,3],[1,2,3]] ，唯一可能的最短 超序列 是 [1,2,3] 。[1,2,3,4] 是可能的超序列，但不是最短的。
如果 nums 是序列的唯一最短 超序列 ，则返回 true ，否则返回 false 。
子序列 是一个可以通过从另一个序列中删除一些元素或不删除任何元素，而不改变其余元素的顺序的序列。

 <!--more-->

[题目链接](https://leetcode.cn/problems/ur2n8P)

示例 1：

```java
输入：nums = [1,2,3], sequences = [[1,2],[1,3]]
输出：false
解释：有两种可能的超序列：[1,2,3]和[1,3,2]。
序列 [1,2] 是[1,2,3]和[1,3,2]的子序列。
序列 [1,3] 是[1,2,3]和[1,3,2]的子序列。
因为 nums 不是唯一最短的超序列，所以返回false。
```



示例 2：

```java
输入：nums = [1,2,3], sequences = [[1,2]]
输出：false
解释：最短可能的超序列为 [1,2]。
序列 [1,2] 是它的子序列：[1,2]。
因为 nums 不是最短的超序列，所以返回false。
```



示例 3：

```java
输入：nums = [1,2,3], sequences = [[1,2],[1,3],[2,3]]
输出：true
解释：最短可能的超序列为[1,2,3]。
序列 [1,2] 是它的一个子序列：[1,2,3]。
序列 [1,3] 是它的一个子序列：[1,2,3]。
序列 [2,3] 是它的一个子序列：[1,2,3]。
因为 nums 是唯一最短的超序列，所以返回true。
```




提示：

- n == nums.length
- 1 <= n <= 104
- nums 是 [1, n] 范围内所有整数的排列
- 1 <= sequences.length <= 104
- 1 <= sequences[i].length <= 104
- 1 <= sum(sequences[i].length) <= 105
- 1 <= sequences[i][j] <= n
- sequences 的所有数组都是 唯一 的
- sequences[i] 是 nums 的一个子序列





### 思路

题目已经明确 `sequences[i] `都是数组`nums`的子序列，因此每个序列中的数字顺序都和 `nums`中的数字顺序一致。为了判断 `nums`是不是序列的唯一最短超序列，只需要判断根据 `sequences` 中的每个序列构造超序列的结果是否唯一。可以将 `sequences` 中的所有序列看成有向图，数字 1 到 n 分别表示图中的 n 个结点，每个序列中的相邻数字表示的结点之间存在一条有向边。根据给定的序列构造超序列等价于有向图的拓扑排序。

- 首先根据有向边计算每个结点的入度，然后将所有入度为 0 的结点添加到队列中，进行拓扑排序。每一轮拓扑排序时，队列中的元素个数表示可以作为超序列下一个数字的元素个数，根据队列中的元素个数，执行如下操作。
- 如果队列中的元素个数大于 1，则超序列的下一个数字不唯一，因此 `nums` 不是唯一的最短超序列，返回 false。
- 如果队列中的元素个数等于 1，则超序列的下一个数字是队列中唯一的数字。将该数字从队列中取出，将该数字指向的每个数字的入度减 1，并将入度变成 0 的数字添加到队列中。

重复上述过程。



### 代码实现

```java
class Solution {
    public boolean sequenceReconstruction(int[] nums, int[][] sequences) {
        int n = nums.length;
        // 每个元素的入度信息
        int[] indegrees = new int[n + 1];
        // 记录元素入度信息是否增加过
        Set<Integer>[] graph = new Set[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new HashSet<>();
        }
        for (int[] sequence : sequences) {
            int size = sequence.length;
            for (int i = 0; i < size - 1; i++) {
                int pre = sequence[i];
                int next = sequence[i + 1];
                // 避免重复增加 入度
                if (!graph[pre].contains(next)) {
                    graph[pre].add(next);
                    indegrees[next]++;
                }
            }
        }
        LinkedList<Integer> queue = new LinkedList<>();
        for (int i = 1; i <= n; i++) {
            if (indegrees[i] == 0) {
                queue.add(i);
            }
        }
        while (!queue.isEmpty()) {
            if (queue.size() > 1) {
                return false;
            }
            int num = queue.pollFirst();
            Set<Integer> set = graph[num];
            for (int element : set) {
                indegrees[element]--;
                if (indegrees[element] == 0) {
                    queue.add(element);
                }
            }
        }
        return true;
    }
}
```

