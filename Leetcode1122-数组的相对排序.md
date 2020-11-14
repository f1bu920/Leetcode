---
title: Leetcode1122.数组的相对排序
date: 2020-11-14 10:34:52
category: Leetcode
tags:
  - 排序
---

## Leetcode1122.数组的相对排序

给你两个数组，`arr1` 和 `arr2`，

`arr2` 中的元素各不相同
`arr2` 中的每个元素都出现在 `arr1` 中
对 `arr1` 中的元素进行排序，使 `arr1` 中项的相对顺序和 `arr2` 中的相对顺序相同。未在 `arr2` 中出现过的元素需要按照升序放在 `arr1` 的末尾。

 [题目链接](https://leetcode-cn.com/problems/relative-sort-array)

<!--more-->

示例：

```
输入：arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
输出：[2,2,2,1,4,3,3,9,6,7,19]
```




提示：

- arr1.length, arr2.length <= 1000
- 0 <= arr1[i], arr2[i] <= 1000
- arr2 中的元素 arr2[i] 各不相同
- arr2 中的每个元素 arr2[i] 都出现在 arr1 中



### 思路

将`arr2`中元素存放到哈希表中，值为key，下标为value，将arr1中元素放进`List`中，按照自定义排序规则排序。

- 如果元素都在arr2中，按照下标进行排序
- 有一个在arr2中，在arr2中的排在前面
- 都不在arr2中，按照数字大小进行排序



### 代码实现

```java
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        if(arr1 == null){
            return arr1;
        }
        if(arr2 == null){
            Arrays.sort(arr1);
            return arr1;
        }
        //存放arr2值和下标的映射
        Map<Integer, Integer> map = new HashMap(arr2.length);
        for (int i = 0; i < arr2.length; i++) {
            map.put(arr2[i], i);
        }
        //存放arr1中元素
        List<Integer> list = new ArrayList<>(arr1.length);
        for (int num : arr1) {
            list.add(num);
        }
        //自定义排序
        Collections.sort(list, (Integer x, Integer y) -> {
            if (map.containsKey(x) || map.containsKey(y)) {
                return map.getOrDefault(x, 1001) - map.getOrDefault(y, 1001);
            }
            return x - y;
        });
        int index = 0;
        for (int num : list) {
            arr1[index++] = num;
        }
        return arr1;
    }
}
```



