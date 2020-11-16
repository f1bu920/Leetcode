---
title: Leetcode406.根据身高重建队列
date: 2020-11-16 13:15:10
category: Leetcode
tags:
  - 排序
---

##  Leetcode406.根据身高重建队列

假设有打乱顺序的一群人站成一个队列。 每个人由一个整数对(h, k)表示，其中h是这个人的身高，k是排在这个人前面且身高大于或等于h的人数。 编写一个算法来重建这个队列。

注意：
总人数少于1100人。

[题目链接](https://leetcode-cn.com/problems/queue-reconstruction-by-height)

<!--more-->

示例

```
输入:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

输出:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```



### 思路

将数组根据身高`h`降序排序，当遇到身高相同时按照`k`升序排序。

排序完成后按照k指定的位置插入到队列中。



### 代码实现

```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (int[] o1, int[] o2) -> {
            return o1[0] == o2[0] ? o1[1] - o2[1] : o2[0] - o1[0];
        });
        List<int[]> list = new LinkedList<>();
        for (int[] p : people) {
            list.add(p[1], p);
        }
        return list.toArray(new int[people.length][2]);
    }
}
```

