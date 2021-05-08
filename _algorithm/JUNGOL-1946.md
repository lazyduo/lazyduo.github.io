---
title: "JUNGOL - 1946 음악프로그램"
date: 2021-05-08 12:17:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - algorithm
    - graph
    - topological sorting
    - BFS
    - cpp
---

**위상정렬(Topological Sorting)** 문제이다. 입력 받을 때, 'Parent' Node의 수를 count 하고, 부모가 없는 Node 부터 `queue`에 넣어 BFS로 탐색한다. 현재 노드에서 갈 수 있는 모든 노드의 'Parent' count를 차감 하고, 만약 count가 0이라면 더 이상 앞에 나올 숫자가 없는 것이므로 `queue`에 넣어 주면 된다.

그리고 정답 배열은 BFS 탐색 과정에서 `queue`에서 `pop()` 할 때 추가해주면 된다.


- [문제 링크](http://www.jungol.co.kr/bbs/board.php?bo_table=pbank&wr_id=1219&sca=5030)

```cpp

/**************************************************************
    Result: Success
    Time:2 ms
    Memory:1284 kb
****************************************************************/
 
 
#include <stdio.h>
#include <vector>
#include <queue>
 
using namespace std;
 
#define MAX 1001
int cnt[MAX], ans[MAX]; // cnt : 들어오는 간선 수
 
int main()
{
    // freopen("input.txt", "r", stdin);
 
    int n, m, u, v, t;
    scanf("%d %d", &n, &m);
    vector<int> edge[n+1];
    while(m--) {
        scanf("%d%d", &t, &u);
            while( --t){
                scanf("%d", &v);
                edge[u].push_back(v);
                cnt[v]++;
                u = v;
            }
    }
 
    int idx = 0;
    queue<int> q;
    // cnt[i]가 0일때만 queue에 들어갈 수 있음.
    for (int i=1; i<=n; i++) if(!cnt[i]) q.push(i);
 
    while( !q.empty())
    {
        u = q.front();
        q.pop();
        ans[idx++] = u;
 
        for (auto v : edge[u])
        {
            if (cnt[v])
            {
                cnt[v]--;
                if (cnt[v] == 0) q.push(v);
            }
        }
    }
 
    if (idx < n) printf("0");
    else
    {
        for (int i=0; i<n; i++)
            printf("%d\n", ans[i]);
    }
    return 1;
}

```