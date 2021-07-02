---
title: "PROGRAMMERS - 도둑질"
date: 2021-07-02 18:06:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - dp
---

또 다시 `dp` 문제. 첫 번째 집을 택하는 것을 'flag'로 가져가야하나? 싶었는데 그냥 가져가는 경우 / 안가져가는 경우 나눠서 `dp` 배열을 두 개로 만들면 되는거였다.

`dp`를 두 번 탐색하게 되니까 `효율성`이 통과하지 못할거라고 생각해서 섣불리 위와 같은 접근을 하기 어려웠는데, 사실 어차피 for문은 처음부터 끝까지 한 번 도는 거고, `memoization`만 dp1, dp2 따로 해주면 되는 것이라서 효율성은 충분히 만족할 수 있었다.

그 외의 핵심 알고리즘은 아무래도 for 문 안에서 업데이트 조건인

```
dp1[i] = max(dp1[i-2] + money[i], dp1[i-1])
```

이 부분이다.

현재 집을 털고 그 전전에서의 max값인 dp\[i-2]와 털지 않고 바로 전에서의 max인 dp\[i-1]과 값을 비교하여 max 값으로 업데이트 해주면 된다!

**Tip** 첫번째 집을 선택하는 dp 배열은 배열 크기를 처음 부터 하나 작게 만드는 것이 나중에라도 안 헷갈린다.

- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42897)

```python
def solution(money):    
    length = len(money)
    dp1 = [0] * (length-1) # 첫번째 집 선택
    dp2 = [0] * length # 첫번째 집 선택 x
    
    dp1[0] = money[0]
    dp1[1] = money[0]
    
    dp2[0] = 0
    dp2[1] = money[1]
    
    for i in range(2, length):
        if (i != length-1):
            dp1[i] = max(dp1[i-2] + money[i], dp1[i-1])
            
        dp2[i] = max(dp2[i-2] + money[i], dp2[i-1])
    
    return max(dp1[-1], dp2[-1])
```
