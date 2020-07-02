---
title: nowcoder.201301 JAVA题目0-1级
date: 2020-06-17 09:46:40
categories: nowcoder
tags:
  - 递归
---

## nowcoder.201301 JAVA题目0-1级

### 题目描述

编写一个函数，传入一个int型数组，返回该数组能否分成两组，使得两组中各元素加起来的和相等，并且，所有5的倍数必须在其中一个组中，所有3的倍数在另一个组中（不包括5的倍数），能满足以上条件，返回true；不满足时返回false。 

[链接](https://www.nowcoder.com/practice/9af744a3517440508dbeb297020aca86?tpId=37&&tqId=21316&rp=1&ru=/ta/huawei&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
第一行是数据个数，第二行是输入的数据
```

### 输出描述:

```
返回true或者false
```

示例1

### 输入

```
4
1 5 -5 1
```

### 输出

```
true
```



### 思路

将能整除5和3的分别分为一组，他们的和分别为`five`和`three`，其他的数字全部放在`nums`中，共有`len`个。

创建递归函数`check(int i, int five, int three, int len, int[] nums)`，其中`five`和`three`分别为两组当前的和，将`nums`中的`len`个数分别分配给这两组，当分配完后，若`five==three`，返回`true`。``i`为即将要分配给这两组的值的下标。**注意`i`尚未分配。**



### 代码实现

```java
import java.io.*;
public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        while ((str = br.readLine()) != null) {
            int n = Integer.parseInt(str);
            String[] strs = br.readLine().split(" ");
            int[] nums = new int[n];
            int five = 0;
            int three = 0;
            int len = 0;
            for(int i = 0;i<n;i++){
                int temp = Integer.parseInt(strs[i]);
                //暂时分为三组，five、three和其他
                if(temp%5==0){
                    five+=temp;
                }else if(temp%3==0){
                    three+=temp;
                }else{
                    nums[len++] = temp;
                }
            }
            System.out.println(check(0,five,three,len,nums));
        }
    }
    //i是即将要分配的下标
    private static boolean check(int i, int five, int three, int len,int[] nums){
        //最后一个数的下标为len-1，这里i==len代表已经全部分配完成
        if(i==len){
            return five==three;
        }
        //将nums[i]分别分配给five和three
        return check(i+1,five+nums[i],three,len,nums)||check(i+1,five,three+nums[i],len,nums);
    }
}
```



