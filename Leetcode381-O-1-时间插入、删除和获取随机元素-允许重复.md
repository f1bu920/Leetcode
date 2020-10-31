---
title: Leetcode381.O(1)时间插入、删除和获取随机元素-允许重复
date: 2020-10-31 11:20:44
categories: Leetcode
tags:
  - 哈希表
  - 设计
---

## Leetcode381.O(1)时间插入、删除和获取随机元素-允许重复


设计一个支持在*平均* 时间复杂度 **O(1)** 下**，** 执行以下操作的数据结构。

**注意: 允许出现重复元素。**

1. `insert(val)`：向集合中插入元素 val。
2. `remove(val)`：当 val 存在时，从集合中移除一个 val。
3. `getRandom`：从现有集合中随机获取一个元素。每个元素被返回的概率应该与其在集合中的数量呈线性相关。

[题目链接](https://leetcode-cn.com/problems/insert-delete-getrandom-o1-duplicates-allowed/)

<!--more-->

**示例:**

```
// 初始化一个空的集合。
RandomizedCollection collection = new RandomizedCollection();

// 向集合中插入 1 。返回 true 表示集合不包含 1 。
collection.insert(1);

// 向集合中插入另一个 1 。返回 false 表示集合包含 1 。集合现在包含 [1,1] 。
collection.insert(1);

// 向集合中插入 2 ，返回 true 。集合现在包含 [1,1,2] 。
collection.insert(2);

// getRandom 应当有 2/3 的概率返回 1 ，1/3 的概率返回 2 。
collection.getRandom();

// 从集合中删除 1 ，返回 true 。集合现在包含 [1,2] 。
collection.remove(1);

// getRandom 应有相同概率返回 1 和 2 。
collection.getRandom();
```





### 思路

使用一个`ArrayList`结构`nums`存储所有的元素列表，使用一个哈希表`Set<Integer, Set<Integer>>`存储每个元素在列表中的下标集合。

获取随机元素时，随机生成一个列表中的索引，即可得到一个随即元素。

插入时记得维护哈希表中的下标集合。

删除元素时由于删除操作不是`O(1)`的，需要将`nums`中最后一个元素与待删除元素交换位置，就可以实现`O(1)`复杂度删除。删除操作需要同时维护数组最后一个元素的下标集合和删除元素的下标集合，还需注意待删除元素就是列表最后一个元素的情况。



### 代码实现

```java
    class RandomizedCollection {
        //Set维护此元素在nums中的下标集合
        Map<Integer, Set<Integer>> idx;
        List<Integer> nums;

        /**
         * Initialize your data structure here.
         */
        public RandomizedCollection() {
            nums = new ArrayList();
            idx = new HashMap();
        }

        /**
         * Inserts a value to the collection. Returns true if the collection did not already contain the specified element.
         */
        public boolean insert(int val) {
            nums.add(val);
            Set<Integer> set = idx.getOrDefault(val, new HashSet<Integer>());
            set.add(nums.size() - 1);
            idx.put(val, set);
            return set.size() == 1;
        }

        /**
         * Removes a value from the collection. Returns true if the collection contained the specified element.
         */
        public boolean remove(int val) {
            if (!idx.containsKey(val)) {
                return false;
            }
            int i = idx.get(val).iterator().next();
            //列表最后一个元素值
            int lastNum = nums.get(nums.size() - 1);
            //更新删除元素的Set下标集合
            idx.get(val).remove(i);
            //交换删除元素与最后一个元素的位置
            nums.set(i, lastNum);
            //更新最后一个元素的下标集合
            idx.get(lastNum).remove(nums.size() - 1);
            //如果nums最后一个元素就是要删除的元素则不用添加
            if (i < nums.size() - 1) {
                idx.get(lastNum).add(i);
            }
            //集合为空时从哈希表中删除
            if (idx.get(val).size() == 0) {
                idx.remove(val);
            }
            nums.remove(nums.size() - 1);
            return true;
        }

        /**
         * Get a random element from the collection.
         */
        public int getRandom() {
            //随机生成一个索引
            return nums.get((int) (Math.random() * nums.size()));
        }
    }
```

