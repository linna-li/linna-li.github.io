---
title: "Cracking the code interview1"
author: "linna.li"
tags: ["basic-knowledge"]
categories: ["book"]
date: 2021-01-13
---

## BackGround

昨天前辈借我一本书让我读，全英文，所以在昨天晚上的第一次尝试就读着读着睡着了。
今晚我来邻居小姐姐家找她一起学习，顺利地读了一部分。前五章是关于interview的介绍，准备，还有行为测试，就先略过了。
前辈的建议是做完每一章的算法题

## Big O 
Big O 是用来描述一个算法有效性的 O() 
空间复杂度，包好了递归函数中用到的变量
可以省略到非主流的部分：O(x!) > O(2^x) > O(x^2) > O(xlogx) > O(x) > O(logx)
### Amortized Time(均摊时间)：

在插入数据到ArrayList的时候，正常是在末尾插入，所以复杂度是O(1), 但是满了之后会扩大容量为两倍，然后复制现有的进去，再进行插入，所以花费的时间是n，所以插入x个数据的时间是：1+2+4+....+x (省略了不需要复制的时候插入消耗的时间)
所以插入每一个花费的时间是 （1+2+4+....+x）/x = 
书上说是 O（1）

### Log N Runtime

### Recursive Runtime
2^0+2^1+....2^n = 2^(n+1) - 1
如果有递归算法的话，一般来说时间都是 O(branched^depth) 

### Example and Exercise
O(N+M) 不可以认为是 O(N)

#### Example 8
有一个String的数组，需要给每一个string自己排序，然后给整个string排序，求时间复杂度
首先第一轮循环把每个string排序。排序每一个string需要的时间是 slogs ， 假设一共是a个，所以一共需要 aslogs。
第二轮是排序这个数组 aloga 次比较，每次比较花费s， 所以是saloga
一共花费时间 aslogs + saloga  ===》 O(as(logs+loga))

#### Example 9
int sum(Node node) {
    if(node == null){
        return 0;
    }
    return sum(node.left) + node.value + sum(node.right);
}
O(2^logN) = 0(N)

#### Example 10
判断一个数是不是质数
boolean isPrime(int n){
    for(int x = 2; x * x <= n;x++){
        if( n%x == 0) {
            return false;
        }
    }
    returrn true;
}
复杂度是: n开方

#### Example 11
int factorial(int n){
    if (n<0) {
        return -1;
    } else if (n==0) {
        return 1;
    } else {
        return n*factorial(n-1)
    }
}
拆开之后是 n * (n-1) * (n-2) *(n-3) *....1，所以是计算n次

#### Example 12
排列(permutation) 


