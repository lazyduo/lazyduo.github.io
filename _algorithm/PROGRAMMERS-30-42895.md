---
title: "PROGRAMMERS - N으로 표현"
date: 2021-10-14 12:21:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - dp
---

언제나 `Dynamic Programming`은 어렵다. 'DP'는 단시간안에 풀라고 만든 문제가 아닌 것 같다.



**Tip** 생각보다 문제에 주어진 조건의 수의 크기가 작으면 완전 탐색과 DP를 고려해 보자.

N을 최대 n번 사용해서 만들 수 있는 수를, 1~n번 까지 차례로 DP에 쌓아 나아가면서 문제를 푼다.
이 때, 최대 8번 초과면 '-1'을 리턴하도록 문제에서 주어져서 해당 for문의 range는 (1,9)로 설정하였다.

N을 i번 사용해서 만들 수 있는 가능 한 수의 집합(set)는 가장 단순히 k번 이어 붙인 것과, 1번으로 만들 수 있는 세트 + (i-1)번으로 만들 수 있는 세트, 2번으로 만들 수 있는 세트 + (i-2)번으로 만들 수 있는 세트 이런식으로 만들 수 있다. 이 때, 나누기의 경우 순서가 중요하므로 순서를 고려하여 1번 세트 + (i-1)번 세트의 결과와 (i-1)번 세트 + 1번 세트 결과가 서로 다름을 인지하자.

- Example
```
5를 3번 사용해서 만들 수 있는 수:
{555} U {1번 세트 + 2번 세트} U {2번 세트 + 1번 세트}
```

이렇게 문제를 이해하면 모든 준비는 끝났다. indexing에 주의하면서 for 문을 돌려주기만 하면 된다.
또한, 최소의 횟수를 구하므로 해당 DP 세트 안에 찾고자 하는 숫자가 있다면, 거기서 for문을 종료하여 현재 스텝인 i를 반환하면 된다.

- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42895)
- [참고](https://gurumee92.tistory.com/164)

```python
def solution(N, number):
    answer = -1
    DP = []
    
    for i in range(1, 9):
        numbers = set()
        numbers.add(int(str(N) * i))
        
        for j in range(0, i-1):
            for x in DP[j]:
                for y in DP[i - 1 - j - 1]: # i-1이 len(DP)와 같아 i-1 생략 가능
                    numbers.add(x + y)
                    numbers.add(x - y)
                    numbers.add(x * y)
                    
                    if y != 0:
                        numbers.add(x // y)
            
        if number in numbers:
            answer = i
            break
                
        DP.append(numbers)
            
    return answer
```