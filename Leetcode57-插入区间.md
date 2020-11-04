---
title: Leetcode57.插入区间
date: 2020-11-04 11:52:48
categories: Leetcode
tags:
  - 模拟
---

## Leetcode57.插入区间

给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

 [题目链接](https://leetcode-cn.com/problems/insert-interval)

<!--more-->

示例 1：

```
输入：intervals = [[1,3],[6,9]], newInterval = [2,5]
输出：[[1,5],[6,9]]
```



示例 2：

```
输入：intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出：[[1,2],[3,10],[12,16]]
解释：这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
```



### 思路

对于区间`[l1, l2]`和区间`[r1, r2]`，如果`l2 < r1`，即第一个区间在第二个区间左侧；如果`l1 > r2`，即第一个区间在第二个区间右侧；如果同时不满足以上条件，则两个区间必定相交。相交区间左端点为两区间左端点最小值，右端点为两区间右端点最大值。

因为给定区间列表无重叠且已按照左端点排序，所以遍历所有区间`[l, r]`：

- 如果r < left，说明当前区间在其左侧，直接加入答案；
- 如果l > right，说明当前区间在其右侧，直接加入答案；
- 如果都不满足，说明出现重叠，更新`newInterval`为合并后的区间。

需要使用一个布尔变量`disPlaced`来判断区间是否已经合并过，如果没有合并过，最后在末尾添加区间。



### 代码实现

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        if(intervals == null || intervals.length < 1){
            return new int[][]{newInterval};
        }
        int left = newInterval[0];
        int right = newInterval[1];
        List<int[]> list = new ArrayList();
        boolean disPlaced = false;
        for(int[] interval : intervals){
            //当前区间在左侧，直接添加
            if(interval[1] < left){
                list.add(interval);
                //当前区间在右侧，添加目标区间和当前区间，使用disPlaced使目标区间只被添加一次
            }else if(interval[0] > right){
                if(!disPlaced){
                    list.add(new int[]{left, right});
                    disPlaced = true;
                }
                list.add(interval);
                //更新合并后的区间
            }else{
                left = Math.min(interval[0], left);
                right = Math.max(interval[1], right);
            }
        }
        //如果目标区间没有被添加过，则在结果末尾添加
        if(!disPlaced){
            list.add(new int[]{left, right});
        }
        int[][] result = new int[list.size()][2];
        int i = 0;
        for(int[] element: list){
            result[i][0] = element[0];
            result[i][1] = element[1];
            i++;
        }
        return result;
    }
}
```



