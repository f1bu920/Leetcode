---
title: Leetcode127.单词接龙
date: 2020-11-05 13:50:19
categories: Leetcode
tags:
  - 广度优先遍历
  - 图
---

## Leetcode127.单词接龙

给定两个单词（`beginWord` 和 `endWord`）和一个字典，找到从 `beginWord` 到 `endWord` 的最短转换序列的长度。转换需遵循如下规则：

每次转换只能改变一个字母。
转换过程中的中间单词必须是字典中的单词。
说明:

如果不存在这样的转换序列，返回 0。
所有单词具有相同的长度。
所有单词只由小写字母组成。
字典中不存在重复的单词。
你可以假设 `beginWord` 和 `endWord` 是非空的，且二者不相同。

[题目链接](https://leetcode-cn.com/problems/word-ladder)

<!--more-->

示例 1:

```
输入:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

输出: 5

解释: 一个最短转换序列是 "hit" -> "hot" -> "dot" -> "dog" -> "cog",
     返回它的长度 5。
```



示例 2:

```
输入:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

输出: 0

解释: endWord "cog" 不在字典中，所以无法进行转换。
```



### 思路

开始时将所有单词添加到集合`set`中，创建`visited`集合代表访问过的节点，创建队列`queue`进行广度优先遍历。



### 代码实现

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        int step = 1;
        int n = beginWord.length();
        //单词列表集合
        Set<String> set = new HashSet(wordList);
        //移除开始单词
        set.remove(beginWord);
        //广度优先遍历队列
        Queue<String> queue = new LinkedList();
        queue.add(beginWord);
        //访问过的集合
        Set<String> visited = new HashSet();
        visited.add(beginWord);
        while(!queue.isEmpty()){
            int size = queue.size();
            //出队
            for(int i = 0;i < size;i++){
                String word = queue.poll();
                char[] charArray = word.toCharArray();
                //遍历每个字符
                for(int j = 0;j < n;j++){
                    //记录原来的字符
                    char originChar = charArray[j];
                    //因为都是小写字母，遍历每个字符
                    for(char k = 'a';k <= 'z';k++){
                        if(k == originChar){
                            continue;
                        }
                        //替换为遍历字符
                        charArray[j] = k;
                        String nextWord = String.valueOf(charArray);
                        //如果单词列表中包含
                        if(set.contains(nextWord)){
                            //找到结尾字符串，直接返回
                            if(endWord.equals(nextWord)){
                                return step + 1;
                            }
                            //要求找到的字符串没被访问过
                            if(!visited.contains(nextWord)){
                                queue.add(nextWord);
                                visited.add(nextWord);
                            }
                        }
                    }
                    //还原为原来的字符
                    charArray[j] = originChar;
                }
            }
            step++;
        }
        //找不到
        return 0;
    }
}
```

