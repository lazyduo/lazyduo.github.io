---
title: "ALGORITHM - Merge Sort"
date: 2021-09-21 15:09:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - sort
    - merge sort
---

`Merge Sort` O(nlogn)을 보장하는 효율적인 정렬 방식.

##  Intro

`Quick Sort`와 마찬가지로 분할 정복을 통해 정렬한다. 배열을 하나의 원소가 될 때 까지 계속 이분할을 먼저 한 후에, 현재 스텝에서 왼쪽 오른쪽 배열의 각 원소를 차례대로 크기순으로 배열한다. 이때 `Merge Sort`가 한 번 일어난 배열은 순서가 정렬된 배열이므로, 두개의 정렬된 배열을 처음 원소 부터 차례로 배열하게 되면 어느 한 쪽 배열이 반드시 먼저 소진되게 되므로 남은 배열은 비교 없이 바로 새로운 배열에 정렬 시킬 수 있다. 왜 O(nlogn)이 되는지는 조금 복잡 할 수 있는데, 우선은 '분할'이 주는 logn이라고 생각해 두자.

## Procedure

1. 배열의 크기가 1이 될 때까지 recursive 하게 Merge Sort를 실행한다.
2. 각 Merge Sort는 중간점을 찾아 배열을 왼쪽 배열과 오른쪽 배열로 이분할 한다.
3. 분할이 끝나면 왼쪽, 오른쪽 배열을 각각의 첫 원소부터 비교해나가면서 각각의 인덱스를 증가시킨다.
4. 어느 한쪽이 끝에 도달하면, 남은 배열은 그대로 (정렬되어 있으니) 새로운 배열에 붙인다.
5. 모든 사이클이 돌면 Merge Sort가 완료된다.

## Code Reference

Github Repo : [source](https://github.com/lazyduo/algorithms-python/blob/main/sort/merge_sort.py)

```python
def mergeSort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2

        L = arr[:mid]
        R = arr[mid:]

        mergeSort(L)
        mergeSort(R)

        i = j = k = 0
    
        # compare left Half and right Half, then sort!
        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1
        
        # handling remain elements
        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1

        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1
```

## Note

`Merge Sort`의 치명적인(?) 단점은 원본 배열만큼의 추가적인 메모리가 필요하단 점이다. 그 이유는 recursive 하게 알고리즘이 돌아가면서 Left, Right 배열을 계속 저장해주고 있어야 하기 때문이다.

또한, 정렬된 배열일지라도 알고리즘 프로세스를 전부 돌아야하는 문제가 있다.

그래도 어떤한 경우에도 O(nlogn)이 보장된다는 점에서는 가장 무난한 효율적인 알고리즘이라고 볼 수 있다.

## 참고

https://www.geeksforgeeks.org/merge-sort/