---
title: nowcoder.计票统计
date: 2020-06-17 08:59:01
categories: nowcoder
tags:
  - 哈希表
  - Array
---

## nowcoder.计票统计

### 题目描述

请实现接口：

unsigned int AddCandidate (char* pCandidateName);
功能：设置候选人姓名
输入： char* pCandidateName 候选人姓名
输出：无
返回：输入值非法返回0，已经添加过返回0 ，添加成功返回1

 

Void Vote(char* pCandidateName);
功能：投票
输入： char* pCandidateName 候选人姓名
输出：无
返回：无


unsigned int GetVoteResult (char* pCandidateName);

功能：获取候选人的票数。如果传入为空指针，返回无效的票数，同时说明本次投票活动结束，释放资源
输入： char* pCandidateName 候选人姓名。当输入一个空指针时，返回无效的票数

输出：无
返回：该候选人获取的票数

 

void Clear()

// 功能：清除投票结果，释放所有资源
// 输入：
// 输出：无
// 返回

 [连接](https://www.nowcoder.com/practice/3350d379a5d44054b219de7af6708894?tpId=37&&tqId=21317&rp=1&ru=/ta/huawei&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入候选人的人数，第二行输入候选人的名字，第三行输入投票人的人数，第四行输入投票。
```

### 输出描述:

```
每行输出候选人的名字和得票数量。
```

示例1

### 输入

```
4
A B C D
8
A B C D E F G H
```

### 输出

```
A : 1
B : 1
C : 1
D : 1
Invalid : 4
```



### 思路

用数组记录输入字符，然后用哈希表存储候选人及其选票数。



### 代码实现

```java
import java.util.*;
import java.io.*;
public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        while((str=br.readLine())!=null){
            int num = Integer.parseInt(str);
            String[] strs = br.readLine().split(" ");
            Map<String,Integer> map = new HashMap(strs.length);
            for(String s:strs){
                map.put(s,0);
            }
            int voteNum = Integer.parseInt(br.readLine());
            int invalid = 0;
            String[] votes = br.readLine().split(" ");
            for(String v: votes){
                if(map.containsKey(v)){
                    map.put(v,map.get(v)+1);
                }else{
                    invalid++;
                }
            }
            for(int i = 0;i<strs.length;i++){
                System.out.println(strs[i]+" : "+map.get(strs[i]));
            }
            System.out.println("Invalid : "+invalid);
        }
    }
} 
```

