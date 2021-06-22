---
title: "PROGRAMMERS - 단어 퍼즐"
date: 2021-06-22 17:29:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - dp
---

`dp` 문제. 언제나 그렇듯.. `dp`는 문제 해결방향을 막 바로 생각해내기가 어렵다.

주어진 문자를 i로 인덱싱하면서, 해당 문자 위치로 끝나는 문자 조각이 있는지 검사한다. (for k ~ 부분)

문자 조각이 있다면, 그 전인 i-k번째 dp값에 1을 더한 값과 현재인 i번째 dp 중 작은 값으로 i번째 dp를 업데이트 한다.

효율성을 위해 문자 조각을 길이 별로 따로 관리할 필요까지는 없다.

(문제에서 문자 조각의 길이가 1이상 5이하라고 주어졌기 때문에, 'k'를 range(1,6)으로 사용)

**Tip** python에서 '무한 값'은 `float('inf')`, `float('-inf')` 로 표현한다.

- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12983)

```python
def solution(strs, t):
    n = len(t)
    dp = [0] * (n + 1)

    for i in range(1, n + 1):
        dp[i] = float('inf')
        
        for k in range(1, 6):
            if i - k < 0:
                continue
            else:
                s = i - k
                
                if t[s:i] in strs:
                    dp[i] = min(dp[i], dp[i - k] + 1)
                
    if dp[-1] == float('inf'):
        answer = -1
    else:
        answer = dp[-1]

    return answer
```
