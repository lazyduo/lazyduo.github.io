---
title: "LeetCode - 121. Best Time to Buy and Sell Stock"
date: 2021-10-22 19:33:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - array
    - leetcode
---

Easy. Blind 75 LeetCode Questions. `Array` 문제는 효율성을 따지면 Time Over가 뜨는 경우가 많으므로 항상 시간 복잡도를 고려해 주어야 한다.

처음 풀이는 배열의 처음 부터 끝까지 3번의 탐색을 거쳐서 풀었다. 현재 index 까지의 최소값과 현재 index 이후의 최댓값 배열을 따로 만든 후, 다시 iteration 하면서 최대의 이윤을 남기는 값을 찾았다.

## 첫 접근

최소, 최대값 배열을 배열의 크기만큼 또 만들어 줘야해서 메모리 낭비도 컸다.

시간복잡도 O(n) * 3에 공간복잡도도 O(n) * 2..

runtime : 1580ms / memory : 25.9MB

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        array_length =len(prices)
        
        asc_min = [10000 for _ in range(array_length)]
        desc_max = [0 for _ in range(array_length)]
        
        curr_min = 10000
        curr_max = 0
        
        for i in range(array_length):
            if prices[i] <= curr_min:
                curr_min = prices[i]
            asc_min[i] = curr_min
            
            if prices[-1-i] >= curr_max:
                curr_max = prices[-1-i]
            desc_max[-1-i] = curr_max
            
        answer = 0
        for i in range(array_length):
            tmp = desc_max[i] - asc_min[i]
            
            if tmp > 0 and tmp > answer:
                answer = tmp
            
        return answer
```

## Brute Force

for문을 2번 돌려서 O(n2)으로 해결하는 방법. 공간 복잡도는 효율적.

LeetCode에서 제공해준 솔루션 중에 하나인데 이 방법을 쓰면 O(n2)이라서 아예 시간초과가 뜬다.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        length = len(prices)
        
        maxProfit = 0
        for i in range(length-1):
            for j in range(i+1, length):
                profit = prices[j] - prices[i]
                
                if profit > maxProfit:
                    maxProfit = profit
                    
        return maxProfit
```

## One Pass

시간 복잡도 O(n)에 공간복잡도 O(1) 솔루션.

한 번의 iteration으로 'maxProfit'을 한 번에 찾을 수 있다.

트릭이라고 한다면, 최소의 가격이랑 최대의 가격을 찾는게 아니라 최소의 가격과 최대의 '이윤'을 찾아가는 것.

runtime : 1080ms / memory : 25.2MB


```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        minPrice = prices[0]
        maxProfit = 0
        
        for price in prices:
            minPrice = min(minPrice, price)
            maxProfit = max(maxProfit, price - minPrice)
                
        return maxProfit
```

