---
title: Leetcode1002.查找常用字符
date: 2020-10-14 10:35:46
categories: Leetcode
tags:
  - 哈希表
---

## Leetcode1002.查找常用字符

给定仅有小写字母组成的字符串数组 A，返回列表中的每个字符串中都显示的全部字符（包括重复字符）组成的列表。例如，如果一个字符在每个字符串中出现 3 次，但不是 4 次，则需要在最终答案中包含该字符 3 次。

你可以按任意顺序返回答案。

 [题目链接](https://leetcode-cn.com/problems/find-common-characters)

<!--more-->

示例 1：

```
输入：["bella","label","roller"]
输出：["e","l","l"]
```



示例 2：

```
输入：["cool","lock","cook"]
输出：["c","o"]
```




提示：

- 1 <= A.length <= 100
- 1 <= A[i].length <= 100
- `A[i][j]`是小写字母



### 思路

利用哈希表存储`A`第一个元素的每个元素出现次数，再依次遍历其他元素。

当`A[0]`出现其他元素中不存在的字符时直接删除，如果都出现相同字符则取出现频率较小的次数为值。



### 代码实现

```java
class Solution {
    public List<String> commonChars(String[] A) {
        List<String> result = new ArrayList();
        //存储第一次遍历中的值，并且作为结果
        Map<Character, Integer> map = new HashMap(32);
        for (char c : A[0].toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        for (int i = 1; i < A.length; i++) {
            char[] chs = A[i].toCharArray();
            Map<Character, Integer> curMap = new HashMap(32);
            for (char c : chs) {
                curMap.put(c, curMap.getOrDefault(c, 0) + 1);
            }
            Iterator<Map.Entry<Character, Integer>> iterator = map.entrySet().iterator();
            //如果出现A[i]中不存在的值，直接删除，否则取较小值
            while (iterator.hasNext()) {
                Map.Entry<Character, Integer> entry = iterator.next();
                char key = entry.getKey();
                if (!curMap.containsKey(key)) {
                    iterator.remove();
                } else {
                    map.put(key, Math.min(map.get(key), curMap.get(key)));
                }
            }
        }
        for (Map.Entry<Character, Integer> entry : map.entrySet()) {
            for (int i = 0; i < entry.getValue(); i++) {
                result.add(String.valueOf(entry.getKey()));
            }
        }
        return result;
    }
}
```



