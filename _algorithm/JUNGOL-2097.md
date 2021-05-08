---
title: "JUNGOL - 2097 지하철"
date: 2021-05-06 23:47:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - cpp
    - algorithm
    - Dijkstra
---

최단 거리 알고리즘 문제. Dijkstra로 풀이 하였으며, 경로 기억을 위한 약간의 코드 추가만 이루어졌다.

Dijkstra 알고리즘을 구현 할 때, 다음 노드를 찾는 과정에서 cpp STL의 `<queue>`에서 **priority_queue**를 사용해야 O(N)을 O(logN)으로 만들 수 있다. 여기서 주의 할 점은 우선 순위 큐를 `reverse`로 사용해야 `.pop()`할 때 가장 작은 값이 나온다.

참고로 Dijkstra 알고리즘의 기본 흐름은 다음과 같다.

1. 우선 순위 큐(pq), 방문을 체크할 배열과 거리를 기록할 배열 생성
2. 시작점 선택 및 우선순위 큐에 삽입 (`emplace`)
3. `!pq.empty()`까지 while문으로 아직 방문하지 정점을 탐색한다. 이 때, 방문 순서는 우선 순위 큐로 부터 나온 '거리가 가장 짧은' 정점 부터 탐색한다.
4. 방문할 때 기록된 거리 보다 거쳐온 길이가 짧으면 거리를 갱신하고 pq에 추가한다.

Dijkstra 알고리즘은 정말 중요한 알고리즘이므로 반드시 알아두자.



**Tip** 문제 링크의 첨부파일 '최단거리알고리즘.pdf'에 관련 알고리즘 들이 정말 잘 정리되어 있다.

- [문제 링크](http://www.jungol.co.kr/bbs/board.php?bo_table=pbank&wr_id=1360&sca=4070)

```cpp

/**************************************************************
    Result: Success
    Time:1 ms
    Memory:1456 kb
****************************************************************/
 
 
#include <stdio.h>
#include <vector>
#include <queue>
 
using namespace std;
 
int g[101][101];
 
 
int main()
{
    int N, M;
    scanf("%d %d", &N, &M);
 
    for (int i=1; i<=N; i++)
    {
        for (int j=1; j<=N; j++)
            {
                scanf("%d", &g[i][j]);
            }
    }
 
    vector<bool> v(N+1); // visit
    vector<int> dist(N+1, 100*101);
    vector<queue<int> > r(N+1);
 
 
    // dijkstra
    priority_queue<pair<int, int>, vector<pair<int, int> >, greater<pair<int, int> > > pq;
 
    pq.emplace(0, 1); // 1에서 시작
    dist[1] = 0;
    r[1].emplace(1);
     
    int u;
    while(!pq.empty())
    {
        u = pq.top().second;
        pq.pop();
        if (v[u]) continue;
 
        v[u] = true;
        for (int i=1; i<=N; i++)
        {
            if (i!=u && !v[i]){
                int newdist = dist[u] + g[u][i];
                if (dist[i] > newdist)
                {
                    dist[i] = newdist;
                    r[i] = r[u];
                    r[i].emplace(i);
                }
                pq.emplace(dist[i], i);                
            }
        }
    }
 
    printf("%d\n", dist[M]);
     
    while (!r[M].empty())
    {
        int x = r[M].front();
        r[M].pop();
        printf("%d ", x);
    }

    return 1;
}
```