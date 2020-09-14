---
title: '50 years, 50 colors'
date: 2019-04-07 21:24:18
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
  - 二分图匹配
---

这个题是最小点覆盖

根据定理也就是求二分图的最大匹配（证明没看懂）

就是我们把行拿出来作为左部分，列拿出来作为右部分，然后两者相连的边就代表了原图中的点

```c++
#include<iostream>
#include<cstdio>
#include<map>
#include<string.h>
using namespace std;
int un,uv;
map<int,int>m;
const int maxn = 100+10;
int g[maxn][maxn];
int linker[maxn];
int used[maxn];
int n,k;
int res[100];
bool dfs(int u,int t){
    for(int v = 0;v<uv;++v){
        if(g[u][v]==t&&!used[v]){
            used[v] = true;
            if(linker[v]==-1||dfs(linker[v],t)){
            linker[v] = u;
            return true;}
        }
    }
    return false;
}
 
int hungry(int t){
    int res = 0;
    memset(linker,-1,sizeof(linker));
    for(int u =0;u<un;++u){
        memset(used,false,sizeof(used));
        if(dfs(u,t))res++;
    }
    return res;
}
int main(){
    while(~scanf("%d%d",&n,&k)&&n+k!=0){
            m.clear();
            un = n,uv= n;
        for(int i = 0;i<n;++i){
            for(int j =0;j<n;++j){
                scanf("%d",&g[i][j]);
                m[g[i][j]]=1;
            }
        }
 
        int h = 0;
        map<int,int>::iterator it;
        for(it = m.begin();it!=m.end();++it){
            if(hungry(it->first)>k){
                res[h++]=it->first;
            }
        }
        if(h==0)
            cout<<-1<<endl;
        else{
                for(int i =0;i<h;++i){
                    if(i)
                        cout<<" "<<res[i];
                    else
                        cout<<res[i];
                }
                cout<<endl;
            }
 
    }
 
}
```

