---
title: "PROGRAMMERS - 무지의 먹방 라이브"
date: 2021-06-21 16:33:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - heapq
---

`heapq`를 import 하여 문제를 해결한다. 완판(싸이클)으로 가장 작은 길이의 접시를 소진할 수 있는지를 'while'문에서 검사한다.

`heapq`라이브러리 활용에 익숙해지는 것이 필요해 보인다. `heapq.heapify()`, `heapq.heappop()`이 어떤식으로 동작하는지 확인하자.

heap에 원소가 없을 경우는 문제 요구 대로 '-1'을 return 하였다.

**Tip** heap에서 첫번째 원소가 가장 작다. 나머지는 트리구조로 되어 있어서 heappop으로 확인하지 않고, 그냥 print 해버리면 순서가 꼬인다.

- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42891)

```python
import heapq

def solution(food_times, k):
    food_times = [(food, idx) for idx, food in enumerate(food_times, 1)]
    heapq.heapify(food_times)
    
    small_food = food_times[0][0]
    prev_food = 0
    
    while k - ((small_food - prev_food) * len(food_times)) >= 0:
        k -= (small_food - prev_food) * len(food_times)
        prev_food = heapq.heappop(food_times)[0]
        if not food_times:
            return -1
        
        small_food = food_times[0][0]
    
    food_times = sorted(food_times, key = lambda x: x[1])
    
    return food_times[k % len(food_times)][1]
```
