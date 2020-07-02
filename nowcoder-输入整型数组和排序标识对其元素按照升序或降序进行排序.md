---
title: nowcoder.输入整型数组和排序标识对其元素按照升序或降序进行排序
date: 2020-06-15 10:10:38
categories: nowcoder
tags:
  - Array
  - 排序
---

## nowcoder.输入整型数组和排序标识对其元素按照升序或降序进行排序

### 题目描述

输入整型数组和排序标识，对其元素按照升序或降序进行排序（一组测试用例可能会有多组数据）

接口说明

原型：

void sortIntegerArray(Integer[] pIntegerArray, int iSortFlag);

输入参数：

Integer[] pIntegerArray：整型数组

int iSortFlag：排序标识：0表示按升序，1表示按降序

输出参数：

无

返回值：

void

[链接](https://www.nowcoder.com/practice/dd0c6b26c9e541f5b935047ff4156309?tpId=37&&tqId=21324&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
1、输入需要输入的整型数个数
```

### 输出描述:

```
输出排好序的数字
```

示例1

### 输入


```
8
1 2 4 9 3 55 64 25
0
```

### 输出


```
1 2 3 4 9 25 55 64
```



### 思路

根据标识符对数组进行顺序或逆序排序。



### 代码实现

```java
import java.io.*;
public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        while((str = br.readLine())!=null){
            int num = Integer.parseInt(str);
            int[] array = new int[num];
            String[] data = br.readLine().split(" ");
            for(int i = 0;i<num;i++){
                array[i] = Integer.parseInt(data[i]);
            }
            int iSortFlag = Integer.parseInt(br.readLine());
            Arrays.sort(array);
            if(iSortFlag==0){
                for(int i = 0;i<array.length;i++){
                    System.out.print(array[i]+" ");
                }
               
            }else{
                for(int i = array.length-1;i>=0;i--){
                    System.out.print(array[i]+" ");
                }
                
            }
            System.out.println();
        }
    }
}
```

