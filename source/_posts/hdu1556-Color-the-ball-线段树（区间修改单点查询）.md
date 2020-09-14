---
title: hdu1556 Color the ball 线段树（区间修改单点查询）
date: 2018-08-04 12:35:14
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
  - 树
  - 线段树
  - hdu
---

---

题意大体就是给你一个区间

然后每次给你一个区间 这个区间内的点加1

问最后每个点的大小是多少

这个地方运用懒节点，区间修改时积累下来 当查询是再对区间修改有影响的点进行修改。

### Color the ball

Time Limit: 3000 ms / Memory Limit: 32768 kb

Description

N个气球排成一排，从左到右依次编号为1,2,3....N.每次给定2个整数a b(a <= b),lele便为骑上他的“小飞鸽"牌电动车从气球a开始到气球b依次给每个气球涂一次颜色。但是N次以后lele已经忘记了第I个气球已经涂过几次颜色了，你能帮他算出每个气球被涂过几次颜色吗？

Input

每个测试实例第一行为一个整数N,(N <= 100000).接下来的N行，每行包括2个整数a b(1 <= a <= b <= N)。
当N = 0，输入结束。

Output

每个测试实例输出一行，包括N个整数，第I个数代表第I个气球总共被涂色的次数。

```
3
1 1
2 2
3 3
3
1 1
1 2
1 3
0
1 1 1
3 2 1
```

---

```c++
#include<cstdio>
using namespace std;
#define fm (t[k].l+t[k].r)>>1
const int maxn=100000+5;
int x,y,a,b;
int ans=0;
struct node
{
    int l,r,w,f;
};
node t[maxn*4+5];
void build(int k,int l,int r)
{
    t[k].l=l;
    t[k].r=r;
    if(t[k].l==t[k].r)
    {
        t[k].w=0;
        t[k].f=0;
        return;
    }
    int m=(t[k].r+t[k].l)>>1;
    build(2*k,l,m);
    build(2*k+1,m+1,r);
    t[k].w=0;
    t[k].f=0;
}
void down(int k)
{
    t[k*2].f+=t[k].f;
    t[k*2+1].f+=t[k].f;
    t[k*2].w+=t[k].f*(t[k*2].r-t[k*2].l+1);
    t[k*2+1].w+=t[k].f*(t[k*2+1].r-t[k*2+1].l+1);
    t[k].f=0;
}
void add(int k)
{
    if(t[k].l>=a&&t[k].r<=b)
    {
        t[k].w+=(t[k].r-t[k].l+1);
        t[k].f+=1;//区间修改时积累f
        return;
    }
   // if(t[k].f) down(k);//在区间修改时不下传
    int m=fm;
    if(a<=m) add(2*k);
    if(b>m) add(2*k+1);
    t[k].w+=t[k*2].w+t[k*2+1].w;
 
}
void ask_point(int k)
{
    if(t[k].l==t[k].r)
    {
        ans=t[k].w;
        return;
    }
    if(t[k].f) down(k);//查询时把点所属于的区间的懒节点积累值下传
    int m=fm;
    if(x<=m) ask_point(2*k);
    else ask_point(2*k+1);
}
int main(void)
{
    int n;
    while(scanf("%d",&n)!=EOF&&n!=0)
    {
        build(1,1,n);
        for(int i=0;i<n;++i)
        {
            scanf("%d%d",&a,&b);
            add(1);
        }
        for(int i=1;i<=n;++i)
        {
            x=i;
            ask_point(1);
            if(i==1)
            printf("%d",ans);
            else
                printf(" %d",ans);
        }
        printf("\n");
    }
 
}
```

