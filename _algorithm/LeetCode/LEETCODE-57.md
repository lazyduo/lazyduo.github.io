---
title: "LeetCode - 57. Insert Interval"
date: 2021-10-23 01:33:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - interval
---

Medium. Blind 75 LeetCode Questions. `Interval`

O(n)으로 해결. 'intervals'를 iteration 하면서 result 스택에 원소들을 추가 시킨다. 이 때 newInterval이 현재 interval에 겹치는 경우 스택에 추가하지 않고 새로운 newInterval을 업데이트 하는 방식으로 overlap을 해결함.

runtime : 121ms / memory : 17.4MB

```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        result = []
        
        for idx, interval in enumerate(intervals):
            if interval[1] < newInterval[0]:
                result.append(interval)
                
            elif interval[0] > newInterval[1]:
                result.append(newInterval)
                result += intervals[idx:]
                break
            
            else: # overlap case. update newInterval
                newInterval[0] = min(newInterval[0], interval[0])
                newInterval[1] = max(newInterval[1], interval[1])
            
        else:
            result.append(newInterval)
        
        return result
```