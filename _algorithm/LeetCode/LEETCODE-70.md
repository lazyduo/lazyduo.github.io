---
title: "LeetCode - 70. Climbing Stairs"
date: 2021-10-21 23:37:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - dp
---

Easy. Blind 75 LeetCode Questions. `Dynamic Programming`의 정말 기초적인 문제로 처음 접하는 사람에게 설명할 때 유용할 문제인 것 같다.

아래의 점화식만 이용하면 된다.

```
f(n) = f(n-2) + f(n-1)
f(1) = 1, f(2)= 2
```

'n'이 1부터 가능하므로 예외 처리로 1 혹은 2일 때는 바로 리턴 시켜 줬다.

runtime : 32ms / memory : 14.3MB

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # f(n) = f(n-2) + f(n-1)
        # f(1) = 1, f(2)= 2

        # exception
        if n == 1 or n == 2:
            return n
        
        # initiate
        DP = [0 for _ in range(n+1)]
        DP[1] = 1
        DP[2] = 2
        
        for i in range(3, n+1):
            DP[i] = DP[i-1] + DP[i-2]
            
        return DP[n]
```