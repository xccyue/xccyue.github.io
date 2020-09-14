---
title: 'divide by three, multiply by two'
date: 2018-07-09 18:49:54
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
  - 思维
  - codeforces
---

---

D. Divide by three, multiply by two

time limit per test

1 second

memory limit per test

256 megabytes

input

standard input

output

standard output

Polycarp likes to play with numbers. He takes some integer number xx, writes it down on the board, and then performs with it n−1n−1 operations of the two kinds:

- divide the number xx by 33 (xx must be divisible by 33);
- multiply the number xx by 22.

After each operation, Polycarp writes down the result on the board and replaces xx by the result. So there will be nn numbers on the board after all.

You are given a sequence of length nn — the numbers that Polycarp wrote down. This sequence is given in arbitrary order, i.e. the order of the sequence can mismatch the order of the numbers written on the board.

Your problem is to rearrange (reorder) elements of this sequence in such a way that it can match possible Polycarp's game in the order of the numbers written on the board. I.e. each next number will be exactly two times of the previous number or exactly one third of previous number.

It is guaranteed that the answer exists.

Input

The first line of the input contatins an integer number nn (2≤n≤1002≤n≤100) — the number of the elements in the sequence. The second line of the input contains nn integer numbers a1,a2,…,ana1,a2,…,an (1≤ai≤3⋅10181≤ai≤3⋅1018) — rearranged (reordered) sequence that Polycarp can wrote down on the board.

Output

Print nn integer numbers — rearranged (reordered) input sequence that can be the sequence that Polycarp could write down on the board.

It is guaranteed that the answer exists.

---

这道题其实就是 按能膜3的数目由高到低排列 因为只有两种方式 一种是除以3一种是乘以2 所以能膜的3的数目肯定是依次递减的

并且 如果相邻的两者膜3的数目相等 那肯定是数小的在前面 数大的在后面 选择的是乘以2的方式

所以pair先比较除以3的数目 再比较乘以2的数目。

```c++
#include<iostream>
#include<cstdio>
#include<algorithm>
using namespace std;
typedef long long ll;
ll n,x;
pair<ll,ll>a[105];
 
int main(void)
{
    ll i,c,t;
    cin>>n;
    for(i=0;i<n;++i)
    {
        cin>>x;
        for(t=x,c=0;t%3==0;t/=3)c++;
        a[i]={-c,x};
 
    }
    sort(a,a+n);
 
    for(int i=0;i<n;++i)
    {
        cout<<a[i].first<<'*';
        cout<<a[i].second<<' ';
    }
    return 0;
 
 
 
}
```