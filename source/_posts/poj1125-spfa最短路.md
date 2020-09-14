---
title: poj1125 spfa最短路
date: 2018-09-19 11:56:44
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
  - 图
  - spfa
  - poj
---

```c++
#include<iostream>
#include<cstdio>
#include<queue>
#include<string.h>
using namespace std;
int inf=0x3f3f3f;
int a[105];
int n;
int mp[105][105];
int dis[105];
int vis[105];
int sum=0x3f3f3f,pot;
void init()
{
    sum=0x3f3f3f;
    memset(mp,0,sizeof(mp));
    for(int i=1;i<=n;++i)
    {
        int m;
        scanf("%d",&m);
        for(int j=1;j<=m;++j)
        {
            int x,y;
            scanf("%d%d",&x,&y);
            mp[i][x]=y;
        }
    }
    for(int i=1;i<=100;++i)
    {
        for(int j=1;j<=100;++j)
        {
            if(mp[i][j]==0&&i!=j)
                mp[i][j]=inf;
        }
    }
}
void spfa(int start)
{
    queue<int>q;
    for(int i=1;i<=n;++i)
    {
        dis[i]=inf;
        vis[i]=false;
    }
    dis[start]=0;
    int now;
    vis[start]=true;
    q.push(start);
    while(!q.empty())
    {
        now=q.front();
        q.pop();
        vis[now]=false;
        for(int i=1;i<=n;++i)
        {
            if(dis[i]>mp[now][i]+dis[now])
            {
                dis[i]=mp[now][i]+dis[now];
                if(vis[i]==0)
                {
                    q.push(i);
                    vis[i]=true;
 
                }
            }
        }
    }
    int sum1=0;
    for(int i=1;i<=n;++i)
    {
        if(dis[i]==inf)
        {
            return;
        }
        if(dis[i]>sum1)
            sum1=dis[i];
    }
    if(sum1<sum)
    {
        sum=sum1;
        pot=start;
    }
 
 
}
int main(void)
{
    while(scanf("%d",&n)&&n)
    {
        init();
        for(int i=1;i<=n;++i)
            spfa(i);
        if(sum==0)
            printf("disjoint\n");
        else
        {
            printf("%d %d\n",pot,sum);
        }
 
    }
}
```

