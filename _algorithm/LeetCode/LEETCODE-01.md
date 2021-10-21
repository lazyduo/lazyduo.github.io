---
title: "LeetCode - 1. Two Sum"
date: 2021-09-08 21:01:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
---

간단하지만은 않은 문제. O(n2) 보다 효율적이게 풀어라!

- O(n2)인 가장 쉬운 접근 법

답은 맞추겠지...

runtime : 5995ms / memory : 14.9MB

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums) - 1):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```

- O(n) : Dictionary(hash map)을 이용해서 애초에 target - num 을 저장해두는 방법.

확실히 빨라지긴했다. 더 효율적인게 있을까?

runtime : 90ms / memory : 15.5MB

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_dic = {}
        for idx, num in enumerate(nums):
            if num_dic.get(num, None) != None :
                return [num_dic[num], idx]
            
            num_dic[target - num] = idx
```