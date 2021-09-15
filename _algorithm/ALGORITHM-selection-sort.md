---
title: "ALGORITHM - Selection Sort"
date: 2021-09-15 16:16:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - sort
    - selection sort
---

`Selection Sort`. Bubble Sort과 거의 비슷하게 간단한 기본적인 정렬 방법.

##  Intro

[`Bubble Sort`](https://lazyduo.github.io/algorithm/ALGORITHM-bubble-sort/)가 인접 원소와 계속해서 비교하면서 자리 스왑이 일어 났다면, 
`Selection Sort`  __정렬에서는 남은 정렬되지 않은 배열에서의 최소(혹은 최대)의 값이랑만 스왑이 한 번 일어 난다.__ 즉, 알고리즘 복잡도는 동일하게 O(n2)이지만, 
스왑이 일어나는 횟수는 최대 n 번으로 메모리 운영 측면에서 조금 더 효율적인 알고리즘이라고 할 수 있다.

## Procedure

1. 첫 원소 인덱스 부터 시작한다.
2. 자신을 포함하는 오른쪽 배열(정렬되지 않은 배열)에서 가장 작은(혹은 큰) 값의 위치를 찾는다.
3. 그 값과 자리를 바꾸고, 다음 인덱스에서 1, 2 과정을 반복한다.

## Code Reference

Github Repo : [source](https://github.com/lazyduo/algorithms-python/blob/main/sort/selection_sort.py)

- 기본형

```python
def slsectionSort(arr):
    for i in range(len(arr)):
        
        min_idx = i
        # find the minimum element idx
        # in remaining unsorted array
        for j in range(i+1, len(arr)):
            if arr[min_idx] > arr[j]:
                min_idx = j
        
        # Swap
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
```

- Stable Selection Sort

'Stable'한 정렬에 관해서는 아래 Note에서 다루겠다.

```python
def stableSlsectionSort(arr):
    for i in range(len(arr)):
        
        min_idx = i
        # find the minimum element idx
        # in remaining unsorted array
        for j in range(i+1, len(arr)):
            if arr[min_idx] > arr[j]:
                min_idx = j
        
        # instead Swapping, insert min to right place
        key = arr[min_idx]
        while min_idx > i:
            arr[min_idx] = arr[min_idx - 1]
            min_idx -= 1
        arr[i] = key
```

## Note

`Stable` 정렬은 같은 크기의 값이라면 처음 배열의 순서를 유지해주어야 한다.

하지만, 기본형의 `Selection Sort`는 '스왑'이 일어나기 때문에, 동일한 값에 대해서 처음 배열의 순서를 보장하지 못한다. 
아래 예시를 보면 '4A'는 '1'과 Swap 되면서 '4B'보다 뒤로 밀려 순서가 틀어지게 된다. 
따라서, Swap(자리 바꿈) 대신에 인덱스를 미는 방법으로 해결해야만, 삽입 정렬이 'Stable`하게 된다.

```bash
Input : 4A 5 3 2 4B 1
Output : 1 2 3 4B 4A 5

Stable Selection Sort would have produced
Output : 1 2 3 4A 4B 5
```

위의 `Stable Selection Sort` Code를 보면 min_idx를 i의 위치로 이동하면서 기존 배열을 while 문에서 그대로 한 칸씩 밀고 있는 것을 볼 수 있다.

## 참고

https://www.geeksforgeeks.org/selection-sort/

https://www.geeksforgeeks.org/stable-selection-sort/
