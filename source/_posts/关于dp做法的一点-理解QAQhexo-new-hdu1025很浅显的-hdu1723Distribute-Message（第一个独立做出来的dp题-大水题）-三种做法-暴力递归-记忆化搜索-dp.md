---
title: >-
  关于dp做法的一点...理解QAQ很浅显的 hdu1723Distribute
  Message（第一个独立做出来的dp题...大水题） 三种做法 暴力递归+记忆化搜索+dp
date: 2018-08-06 20:49:17
author: Chaoyue Xing
img: 
top: false
cover: false
coverImg: 
password: 
toc: false
mathjax: false
summary:
categories: Algorithm
tags: 
  - dp
  - hdu
---

---

# **Distribute Message**

***\**\*Time Limit: 1000/1000 MS (Java/Others)  Memory Limit: 32768/32768 K (Java/Others)
Total Submission(s): 2276  Accepted Submission(s): 1144\*\**\***

 

Problem Description

The contest’s message distribution is a big thing in prepare. Assuming N students stand in a row, from the row-head start transmit message, each person can transmit message to behind M personals, and how many ways could row-tail get the message?

 

 

Input

Input may contain multiple test cases. Each case contains N and M in one line. (0<=M<N<=30)
When N=0 and M=0, terminates the input and this test case is not to be processed.

 

 

Output

Output the ways of the Nth student get message.

 

 

Sample Input

```
 
```

4 1

4 2

0 0

 

 

Sample Output

```
 
```

1

3

```
 
```

*Hint*

4 1 : A->B->C->D 4 2 : A->B->C->D, A->C->D, A->B->D

---

可以说是很水的一道题目了 但是看了一个关于dp的视频之后终于对dp有点理解了 之前对dp一头雾水不知道从哪里下手

一直搜题解报告动态转移方程才能敲出来这样子

直到看了三个题解之后我看了一个视频 （我查了查是七月在线的动态规划实战课，也不是很贵）

dp定义啊之类的网上很多 就不再copy了 我就说说dp的做法吧（也是刚看的视频教程里面说的）

1.先找到最暴力的解法，然后去除冗余（这里我就用最暴力的方法写了一个递归，从上到下的（n到1），感觉从下到上（1到n）很难找到那个关系）

2.设计并存储状态（一维，二维，三维数组，map，其实这里我刚做这个题的时候并没有想到要几维，写完了记忆化搜索动态转移方程基本就出来了）

3.递归式（转移方程）

4.自底向上计算最优解（编程方式）

如果没思路的话，就先写一遍暴力吧！

附代码

```c++

#include<iostream>
#include<cstdio>
using namespace std;
int rf(int m,int n)
{
    int sum=0;
    if(n==1)
        return 1;
    for(int i=1;i<=m;++i)
    {
        if(n-i>=1)
            sum+=rf(m,n-i);
    }
    return sum;
}
int main(void)
{
    int n,m;
    while(scanf("%d%d",&n,&m)!=EOF&&n+m!=0)
    {
       int h= rf(m,n);
       printf("%d\n",h);
    }
 
}
```

