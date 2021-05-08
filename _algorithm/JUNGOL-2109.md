---
title: "JUNGOL - 2109 꿀꿀이 축제"
date: 2021-05-08 10:11:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - algorithm
    - graph
    - dijkstra
    - cpp
---

`Dijkstra`를 두 번 쓰는 문제다. '꿀꿀이'들이 오고 가고 했을 때 총합이 작아야 하고, 이 총합 중에서 `max` 값을 갖는 꿀꿀이의 거리를 구하는 문제.

여기서 포인트는 `Dijkstra` 알고리즘을 쓸 때, 반드시 **도착점**을 같이 받아 도착점을 방문하면 빠져나오게 해야 시간을 줄일 수 있다.

`if (u.second == end) break;` (도착점 처리 부분)

그렇게 해서 '출발점->도착점', '도착점->출발점' `Dijkstra`를 두번 돌리면 된다!

**Tip** Dijkstra 숙지는 필수!

- [문제 링크](http://www.jungol.co.kr/bbs/board.php?bo_table=pbank&wr_id=2341&sca=4070)

```cpp
/**************************************************************
    Result: Success
    Time:136 ms
    Memory:5348 kb
****************************************************************/
 
 
#include <stdio.h>
#include <vector>
#include <queue>
 
using namespace std;
 
#define MAX 1001
#define INF 100000
int g[MAX][MAX];
vector<int> child[MAX];
 
int dijkstra(int n, int start, int end)
{
    // pair <dist, node idx>
    priority_queue<pair<int, int>, vector<pair<int, int> >, greater<pair<int, int> > > pq;
    vector<bool> v(n+1);
    vector<int> dist(n+1, INF);
 
    pq.emplace(0, start);
    dist[start] = 0;
 
    while (!pq.empty()) {
        auto u = pq.top();
        pq.pop();
 
        if (u.second == end) break;
 
        if (v[u.second]) continue;
 
        v[u.second] = true;
 
        for (auto x : child[u.second])
        {
            int newdist = g[u.second][x] + dist[u.second];
            if (!v[x] && dist[x] > newdist)
            {
                dist[x] = newdist;
                pq.emplace(newdist, x);
            }
        }
    }
    return dist[end];
 
}
 
int main()
{
    // freopen("input.txt", "r", stdin);
 
    int n, m, x;
 
    scanf("%d %d %d", &n, &m, &x);
 
 
 
    for (int i=0; i<m; i++)
    {
        int sn, en, w;
        scanf("%d %d %d", &sn, &en, &w);
 
        g[sn][en] = w;
        child[sn].emplace_back(en);
    }
 
    int max = 0;
    for (int i=1; i<=n; i++)
    {
        if (i == x) continue;
 
        int total_dist=0;
        total_dist += dijkstra(n, i, x);
        total_dist += dijkstra(n, x, i);
        if (total_dist > max)
            max = total_dist;
    }
 
    printf("%d", max);
    return 1;
}