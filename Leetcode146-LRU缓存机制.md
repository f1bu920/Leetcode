---
title: Leetcode146.LRU缓存机制
date: 2020-05-25 12:22:20
categories: Leetcode
tags:
  - 设计
  - 哈希表
  - 链表
---

## Leetcode146.LRU缓存机制

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 `get` 和 写入数据 `put` 。

获取数据 `get(key)` - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 `put(key, value)` - 如果密钥已经存在，则变更其数据值；如果密钥不存在，则插入该组「密钥/数据值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

 [题目链接](https://leetcode-cn.com/problems/lru-cache)

<!--more-->

示例:

```
LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得密钥 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得密钥 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4
```



#### 思路

此题中存储方式是K-V式的，所以需要用到`HashMap`，要求时间复杂度为`O(1)`，所以需要用到双向链表。Java中提供了`LinkedHashMap`，也可以自己实现。其中，头部元素是最近使用过的，尾部元素是最久没用过的。每次操作过后，都要把操作的节点移到链表头部。`put`元素时，先判断是否存在，若存在则更新；不存在则插入，都要把节点移到链表头部。如果插入时发现`size>capacity`，则要删除链表尾部元素。



#### 代码实现

```java
public class LRUCache {
    //设计的双向链表节点
    class LRUNode {
        int key;
        int value;
        LRUNode pre;
        LRUNode next;

        public LRUNode() {
        }

        public LRUNode(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    //链表容量
    private int capacity;
    //大小
    private int size;
    //虚拟头尾节点
    private LRUNode head, tail;
    //存储元素的哈希表
    private Map<Integer, LRUNode> cache = new HashMap<>();

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        head = new LRUNode();
        tail = new LRUNode();
        head.next = tail;
        tail.pre = head;
    }
    
    public int get(int key) {
        //判断是否为空，为空则返回-1
        LRUNode node = cache.get(key);
        if (node == null) {
            return -1;
        }
        //移到头部
        moveNodeToHead(node);
        return node.value;
    }

    public void put(int key, int value) {
        LRUNode node = cache.get(key);
        //为空则新建节点
        if (node == null) {
            LRUNode newNode = new LRUNode(key, value);
            size++;
            //插入到HashMap中
            cache.put(key, newNode);
            //插入到链表头部
            addToHead(newNode);
            //删除链表尾部元素
            if (size > capacity) {
                LRUNode removedNode = removeTail();
                //HashMap中也要删除
                cache.remove(removedNode.key);
                size--;
            }
            //不为空则更新
        } else {
            node.value = value;
            //HashMap中也要更新
            cache.put(key, node);
            //删除节点并将节点移到头部
            moveNodeToHead(node);
        }
    }
    //删除节点
    private void removeNode(LRUNode node) {
        node.pre.next = node.next;
        node.next.pre = node.pre;
    }
    //新插入节点插入到头部
    private void addToHead(LRUNode node) {
        node.next = head.next;
        node.pre = head;
        head.next.pre = node;
        head.next = node;
    }
    //删除已存在节点并移到链表头部
    private void moveNodeToHead(LRUNode node) {
        removeNode(node);
        addToHead(node);
    }
    //删除尾部节点
    private LRUNode removeTail() {
        LRUNode nodeToRemove = tail.pre;
        removeNode(tail.pre);
        return nodeToRemove;
    }
}
/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

