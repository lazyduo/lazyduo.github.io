---
title: "LeetCode - 2. Add Two Numbers"
date: 2021-09-10 00:45:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
---

주어진 `Linked List` 클래스의 Traversal과, 숫자를 다시 `Linked List`로 만드는 것이 관건.

Leet Code의 Python3 코드 형태가 아직 익숙하지 않아서 헤맸다. 시간과 메모리가 상위에 들지 않아 더 효율적인 코드가 있을 듯 하다.

runtime : 101ms / memory : 14.1MB

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        num1 = self.traverse_list(l1)
        num2 = self.traverse_list(l2)
        
        answer = num1 + num2
        
        return self.set_list_node(answer)
        
    def traverse_list(self, list_node):
        num = ''
        num += str(list_node.val)
        
        while list_node.next != None:
            list_node = list_node.next
            num += str(list_node.val)
            
        return int(num[::-1])
    
    def set_list_node(self, num):
        prev = None
        for node in str(num):
            curr = ListNode(node, prev)
            prev = curr
        
        return curr
```