---
title: "ALGORITHM - Bubble Sort"
date: 2021-09-10 13:15:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - sort
    - bubble sort
---

'Sort' 알고리즘의 기본. `Bubble Sort`

##  Intro

가장 간단한 정렬 방법이다. 배열을 Linear하게 탐색하면서 바로 옆의(adjacent)의 원소와 비교하여 자리를 바꾼다.
정렬 과정에서 큰(혹은 작은) 원소가 배열의 끝으로 점점 올라가는 형태가 마치 거품이 수면으로 올라오는 모습과 같아 `Bubble Sort`라고 불린다.

모든 인덱스에서 배열의 한 쪽 끝으로 탐색이 이루어지므로 n + (n-1) + ... + 2 + 1 = O(n2)의 복잡도를 갖는다.

## Procedure

1. 매 차수는 0번 원소부터 확인을 시작한다.
2. 인덱스를 증가 시키면서 현재 원소가 바로 다음 원소보다 크다면 서로 Swap 한다.
3. 매 차수 마다 (가장 큰 원소는 가장 끝에 배열 되므로) 가장 큰 원소는 자리가 확정 되므로, 자신의 차수 전까지만 인덱스를 증가시킨다. (n-i)의 이유
4. 배열의 크기 만큼 위 과정을 반복한다. (for i in range(n))

## Code Reference

Github Repo : [source](https://github.com/lazyduo/algorithms-python/blob/main/sort/bubble_sort.py)

- 기본형

```python
def bubbleSort(arr):
    n = len(arr)

    # Number of step
    for i in range(n):

        # Last i elements are already in place
        for j in range(0, n-i-1):

            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

```

- 최적화

```python
def bubbleSort(arr):
    n = len(arr)

    # Number of step
    for i in range(n):
        swapped = False

        # Last i elements are already in place
        for j in range(0, n-i-1):

            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True

            if swapped == False:
                break
```

## Note

최적화된 Code는 swap flag를 두어서, for 문 진행 도중 swap이 한 번도 일어나지 않는 차수가 있으면 거기서 알고리즘을 끝낸다. 
Swap이 일어나지 않으면 정렬이 되어 있다는 의미 이므로, 그 다음 차수를 진행할 필요가 없기 때문이다.

이 방법은 최악의 경우인 reversed sorted의 경우에는 똑같은 시간이 소요되지만, 이미 정렬된 배열의 경우 O(n) 만으로 알고리즘을 끝낼 수 있다.

## 참고

https://www.geeksforgeeks.org/bubble-sort/
