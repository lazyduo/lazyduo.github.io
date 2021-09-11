---
title: "ALGORITHM - Binary Tree"
date: 2021-09-11 20:58:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - tree
    - binary tree
---

python에서 Tree 클래스를 세팅하는 법을 알아 보자.

##  Intro

Binary Tree는 항상 left, right 두 개의 Child가 있다고 보면 된다. 만약 문제에서 어떤게 left인지, Right인지 구분을 하지 않는다면, 단순하게 class에다가 children property를 만들어서 리스트에 추가하는 식으로 추가하면 된다.

## Procedure

생략

## Code Reference

Github Repo : [source](https://github.com/lazyduo/algorithms-python/blob/main/tree/binary_tree.py)

- 일반적인 Binary Tree

```python
class Node:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.value = key

def inorder_traversal(root):
    if root:
        inorder_traversal(root.left)
        print(root.value),
        inorder_traversal(root.right)

def preorder_traversal(root):
    if root:
        print(root.value),
        preorder_traversal(root.left)
        preorder_traversal(root.right)

def postorder_traversal(root):
    if root:
        postorder_traversal(root.right)
        print(root.value),
        postorder_traversal(root.left)
```

- Child가 여럿일때(?)

```python
class Node:
    def __init__(self, key):
        self.children = []
        self.value = key

    def addChild(self, child):
        self.children.append(child)
```

## Note

value 값으로 부터 `Node`를 찾는 방법을 생각해 보자.
순서대로 리스트에 `Node`를 추가하는 것도 좋은 방법일듯.

## 참고

https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/
