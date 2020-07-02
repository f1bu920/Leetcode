---
title: nowcoder.在字符串中找出连续最长的数字串
date: 2020-06-18 16:54:50
categories: nowcoder
tags:
  - String
---

## nowcoder.在字符串中找出连续最长的数字串

### 题目描述

样例输出

输出123058789，函数返回值9

输出54761，函数返回值5

 

接口说明

函数原型：

  unsignedint Continumax(char** pOutputstr, char* intputstr)

输入参数：
  char* intputstr 输入字符串；

输出参数：
  char** pOutputstr: 连续最长的数字串，如果连续最长的数字串的长度为0，应该返回空字符串；如果输入字符串是空，也应该返回空字符串； 

返回值：
 连续最长的数字串的长度

 [题目链接](https://www.nowcoder.com/practice/2c81f88ecd5a4cc395b5308a99afbbec?tpId=37&&tqId=21315&rp=1&ru=/ta/huawei&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入一个字符串。
```

### 输出描述:

```
输出字符串中最长的数字字符串和它的长度。如果有相同长度的串，则要一块儿输出，但是长度还是一串的长度
```

示例1

### 输入

```
abcd12345ed125ss123058789
```

### 输出

```
123058789,9
```



### 思路

使用两个变量`maxLen`和`curLen`分别表示最大长度和当前长度，遍历字符串，若遍历到数字字符，使用`start`记录当前下标，直到遍历下一个非数字字符，计算现在下标到`start`的距离，即为当前长度。

使用一个`List`集合来存储最大长度的字串，如果当前字串长度大于之前的最大长度，则需要清空集合。



### 代码实现

```java
import java.io.*;
import java.util.*;
public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        while((str = br.readLine())!=null){
            int len = str.length();
            ArrayList<String> stack = new ArrayList<String>();
            int maxLen = 0;
            for(int i = 0;i<len;i++){
                char c = str.charAt(i);
                int start = i;
                while(i<len&&Character.isDigit(str.charAt(i))){
                    i++;
                }
                int curLen = i-start;
                if(curLen>maxLen){
                    maxLen = curLen;
                    if(!stack.isEmpty()){
                        stack.clear();
                    }
                    stack.add(str.substring(start,i));
                }else if(curLen==maxLen){
                    stack.add(str.substring(start,i));
                 }
            }
            for(int i = 0;i<stack.size();i++){
                System.out.print(stack.get(i));
            }
            System.out.println(","+maxLen);
        }
    }
}
```

