---
title: "JUNGOL - 1257 전깃줄(중)"
date: 2021-05-06 22:57:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - LIS
    - cpp
---

- [문제 링크](http://www.jungol.co.kr/bbs/board.php?bo_table=pbank&wr_id=540&sca=99&sfl=wr_hit&stx=1257)

**최장 증가 부분 수열(LIS:Longest Increasing Subsequence)** 응용 문제다. LIS 구현할 때, 다음 숫자를 업데이트 시킬 위치를 찾는 과정에서 cpp STL `<algorithm>`의 `lower_bound()`를 이용해 O(LogN)으로 처리해야만 전체 O(NlogN)으로 시간 통과할 수 있다.

또한, 전깃줄을 지워 나갈 때 어떤 경로로 지우는지 알기 위해서 `<map>`으로 Path를 기록해야하 한다.

**Tip** cpp의 `<map>`은 python의 Dictionary와는 다르게 넣으면서 자동으로 정렬 된다.

```cpp
/**************************************************************
    Problem: 1257
    User: dadanuna
    Language: C++
    Result: Success
    Time:233 ms
    Memory:16604 kb
****************************************************************/
 
#include <stdio.h>
#include <map>
#include <vector>
#include <algorithm>
 
using namespace std;
 
int main()
{
    // freopen("input.txt", "r", stdin);
 
    int N; // 전깃줄 개수
    scanf("%d", &N);
 
    map<int, int> mA; // A가 키가 되는 map
    map<int, int> mB;
     
    for (int n = 0; n < N; n++)
    {
        int A, B;
        scanf("%d %d", &A, &B);
        mA.emplace(A, B);
        mB.emplace(B, A);
    }
 
    vector<int> dpMemo;
    dpMemo.reserve(N);
    map<int, int> path;
 
    for (auto& t : mA) {
        int val = t.second;
        int idx = lower_bound(dpMemo.begin(), dpMemo.end(), val) - dpMemo.begin();
 
        if (!dpMemo.size() || idx == dpMemo.size()) {
            dpMemo.emplace_back(val);
        }
        else {
            dpMemo[idx] = val;
        }
 
        path.emplace(val, idx == 0 ? -1 : dpMemo[idx - 1]);
    }
 
    printf("%d\n", N - dpMemo.size());
    int end = dpMemo.back();
 
    while (end != -1) {
        mA.erase(mB[end]);
        end = path[end];
    }
 
    for (auto& t : mA) {
        printf("%d\n", t.first);
    }
     
    return 1;
}
```