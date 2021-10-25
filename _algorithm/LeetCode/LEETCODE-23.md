---
title: "LeetCode - 23. Merge k Sorted Lists"
date: 2021-10-25 15:39:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - linked list
---

Hard. Blind 75 LeetCode Questions. `Linked List`

## 1. Brute Force

단순하게 주어진 'ListNode'들의 모든 노드들을 탐색하여 따로 리스트에 저장해 둔 후, 마지막에 이 리스트를 정렬하여 오름차순으로 새로운 연결 리스트를 만들어 반환한다.

1회 정렬로 인한 O(NlogN) 시간 복잡도를 갖는다.

runtime : 99ms / memory : 18.3MB

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        self.nodes = []
        
        head = point = ListNode(0)
        
        for l in lists:
            while l:
                self.nodes.append(l.val)
                l = l.next
        
        for x in sorted(self.nodes):
            point.next = ListNode(x)
            point = point.next
            
        return head.next
```

## 2. Compare One by One 

k개의 노드리스트를 매번 가장 작은 값을 찾아 결과 배열에 추가하는 형태.

k개 중에 가장 작은 값을 총 노드의 개수인 N번 찾아야 하므로 O(kN)

## 3. Optimize version of 2.

LeetCode에서 주어진 솔루션이 틀릴수도 있다는 것을 알았다. python3 부터는 heapq 혹은 queue에서 비교 가능한 클래스를 따로 정의해서 전달해야만 제대로 put된다. 따라서,  ListNode의 대소 비교를 위해 따로 정의를 추가해주어야 했고, entry에 다시 추가할 때는 현재 node가 아닌 next node를 넣어야지만 제대로 돌아간다.

runtime : 278ms / memory : 18.4MB

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
from queue import PriorityQueue

class PriorityEntry:
    def __init__(self, val, node):
        self.val = val
        self.node = node
        
    def __lt__(self, other):
        return self.val < other.val

class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        self.nodes = []
        
        head = point = ListNode(0)
        q = PriorityQueue()
        
        for l in lists:
            if l:
                q.put(PriorityEntry(l.val, l.next))
        
        while not q.empty():
            entry = q.get()
            val, node = entry.val, entry.node
            point.next = ListNode(val)
            point = point.next
            
            if node:
                q.put(PriorityEntry(node.val, node.next))
            
        return head.next
```

## 4. Merge lists one by one

두 개의 연결 리스트 머지하는 것을 k-1번 실행하는 방법. O(kN)

## 5. Merge with Divide Conquer

왜 Merge2Lists 중간에 이상하게 꼬아서 풀이를 했는지 모르겠다. 그 부분은 자체적으로 좀 바꿨다. 시간복잡도가 O(Nlogk)로 k가 작고 N이 크다면 가장 좋은 효율을 보여줄 수 있는 풀이 방법이고, 가장 적은 공간 복잡도를 갖는다.

runtime : 145ms / memory : 17.8MB

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        amount = len(lists)
        interval = 1
        
        while interval < amount:
            for i in range(0, amount - interval, interval*2):
                lists[i] = self.merge2Lists(lists[i], lists[i + interval])
            interval *= 2
                
        return lists[0] if amount > 0 else None
    
    def merge2Lists(self, l1, l2):
        head = point = ListNode(0)
        
        while l1 and l2:
            if l1.val <= l2.val:
                point.next = l1
                l1 = l1.next
            else:
                point.next = l2
                l2 = l2.next
                
            point = point.next
            
        if not l1:
            point.next = l2
            
        else:
            point.next = l1
        
        return head.next
```


