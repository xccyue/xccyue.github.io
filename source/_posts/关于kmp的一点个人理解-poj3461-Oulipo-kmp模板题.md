---
title: 关于kmp的一点个人理解 poj3461 Oulipo (kmp模板题)
date: 2018-08-04 12:29:03
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
  - 字符串
  - kmp
  - poj
---

---

这个题就是先给子串，然后给母串，问子串在母串中出现的次数。

### Oulipo

Time Limit: 1000 ms / Memory Limit: 32768 kb

Description

The French author Georges Perec (1936–1982) once wrote a book, La disparition, without the letter 'e'. He was a member of the Oulipo group. A quote from the book:

Tout avait Pair normal, mais tout s’affirmait faux. Tout avait Fair normal, d’abord, puis surgissait l’inhumain, l’affolant. Il aurait voulu savoir où s’articulait l’association qui l’unissait au roman : stir son tapis, assaillant à tout instant son imagination, l’intuition d’un tabou, la vision d’un mal obscur, d’un quoi vacant, d’un non-dit : la vision, l’avision d’un oubli commandant tout, où s’abolissait la raison : tout avait l’air normal mais…

Perec would probably have scored high (or rather, low) in the following contest. People are asked to write a perhaps even meaningful text on some subject with as few occurrences of a given “word” as possible. Our task is to provide the jury with a program that counts these occurrences, in order to obtain a ranking of the competitors. These competitors often write very long texts with nonsense meaning; a sequence of 500,000 consecutive 'T's is not unusual. And they never use spaces.

So we want to quickly find out how often a word, i.e., a given string, occurs in a text. More formally: given the alphabet {'A', 'B', 'C', …, 'Z'} and two finite strings over that alphabet, a word W and a text T, count the number of occurrences of W in T. All the consecutive characters of W must exactly match consecutive characters of T. Occurrences may overlap.
 

Input

The first line of the input file contains a single number: the number of test cases to follow. Each test case has the following format:

One line with the word W, a string over {'A', 'B', 'C', …, 'Z'}, with 1 ≤ |W| ≤ 10,000 (here |W| denotes the length of the string W).
One line with the text T, a string over {'A', 'B', 'C', …, 'Z'}, with |W| ≤ |T| ≤ 1,000,000.

Output

For every test case in the input file, the output should contain a single number, on a single line: the number of occurrences of the word W in the text T.

---

```
3
BAPC
BAPC
AZA
AZAZAZA
VERDI
AVERDXIVYERDIAN
```

```
1
3
0
```

```c++
#include<iostream>
#include<cstdio>
#include<cstring>
using namespace std;
const int maxn=10000005;
int knext[maxn];
char s[maxn],t[maxn];
int slen,tlen;
void getnext()
{
    int j,k;
    j=0;k=-1;knext[0]=-1;
    while(j<tlen)
    {
        if(k==-1||t[j]==t[k])
        {
            knext[++j]=++k;
 
        }
        else
            k=knext[k];
    }
}
int count_kmp()
{
    int i=0,k=0;
    int ans=0;
    int j=0;
    if(slen==1&&tlen==1)
    {
        if(s[0]==t[0])
            return 1;
        else
            return 0;
    }
    getnext();
    for(i=0;i<slen;++i)
    {
        while(j>0&&s[i]!=t[j])
            j=knext[j];
        if(s[i]==t[j])
            j++;
        if(j==tlen)
        {
            ans++;
            j=knext[j];
        }
    }
    return ans;
}
int main(void)
{
    int a;
  scanf("%d",&a);
    while(a--)
    {
        scanf("%s",t);
        scanf("%s",s);
        slen=strlen(s);
        tlen=strlen(t);
        printf("%d\n",count_kmp());
    }
}
```

