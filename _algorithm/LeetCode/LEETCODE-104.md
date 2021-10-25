---
title: "LeetCode - 104. Maximum Depth of Binary Tree"
date: 2021-10-24 14:44:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - tree
---

Easy. Blind 72 LeetCode Questions. `Tree`

O(n)으로 해결. stack에 현재의 level(depth)를 같이 리스트나 튜플 형태로 묶어서 준다. while 과정에서 'maxdepth'가 발견됐을 시에 업데이트를 해주면 된다. 구현한 코드는 '전위 순회(preorder traverse)' 형태로 구현되어 모든 트리 노드를 방문한다.

LeetCode python 문제에서 특이한 부분은 인풋 타입과 아웃풋 타입이 정해져 있는 것인데, 잘 모르면 헷갈릴 수 있으니 익숙해지도록 하자.

```python
def maxDepth(self, root: Optional[TreeNode]) -> int:   
```

위의 표현식에서 root는 optional로 None 혹은 TreeNode 클래스가 리스트 형태로 들어온다는 의미이고, return은 int로 해주어야 한다는 의미이다.

runtime : 40ms / memory : 15.4MB

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:        
        if not root:
            return 0
        
        stack = []
        stack.append([root, 1])
        
        maxdepth = 1
        while stack:
            curr = stack.pop()
            maxdepth = max(maxdepth, curr[1])
            
            if curr[0].left:
                stack.append([curr[0].left, curr[1] + 1])
                
            if curr[0].right:
                stack.append([curr[0].right, curr[1] + 1])
        
        return maxdepth
```