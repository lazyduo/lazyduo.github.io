---
title: "ALGORITHM - Insertion Sort"
date: 2021-09-17 13:52:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - sort
    - insertion sort
---

`Insertion Sort`. 도서관 사서가 책을 정리하듯이 매 스텝에서 원소의 적절한 위치를 찾아서 넣는 방법.

##  Intro

`Insertion Sort`  __삽입 정렬에서는 남은 정렬되지 않은 배열의 첫번째 원소를 정렬된 배열의 마지막 원소 부터 비교하면서 적절한 위치를 찾아 삽입한다.__ 
기본 형태의 삽입 정렬 알고리즘은 버블, 선택 정렬 등과 마찬가지로 O(n2)의 복잡도를 갖는다.

## Procedure

1. 정렬 되지 않은 배열의 첫 원소부터 시작한다.
2. 정렬된 배열에서 마지막 원소부터 비교하여 1번에서의 원소가 들어갈 자리를 찾는다.
3. 1번 원소가 들어갈 자리에 원소를 넣어주면서, 해당 위치 뒤로는 하나씩 밀어 준다.
4. 1~3 을 반복한다.

## Code Reference

Github Repo : [source](https://github.com/lazyduo/algorithms-python/blob/main/sort/insertion_sort.py)

- 기본형

```python
def insertionSort(arr):
    for i in range(1, len(arr)):
        j = i - 1
        key = arr[i]

        while j >= 0 and arr[j] > key:
            arr[j+1] = arr[j]
            j -= 1

        arr[j+1] = key
```

- Binary Insertion Sort

현재 원소의 적절한 위치를 찾는 과정을 Binary Search를 활용하면, 비교 횟수를 O(n)에서 O(logn)으로 줄일 수 있다.
하지만 최악의 경우(역순 배열) O(n2)의 복잡도를 갖는 것은 동일하다.

```python
def binaryInsertionSort(arr):
    for i in range(1, len(arr)):
        j = i - 1
        key = arr[i]

        loc = 0
        end = j

        while loc <= end:
            mid = loc + (end - loc) // 2
            if key == arr[mid]:
                loc = mid + 1
                break
            elif key > arr[mid]:
                loc = mid + 1
            else:
                end = mid - 1

        while j >= loc:
            arr[j+1] = arr[j]
            j -= 1
        arr[j + 1] = key
```

## Note

[`Stable Selection Sort`](https://lazyduo.github.io/algorithm/ALGORITHM-selection-sort/#code-reference)와 유사한 방식으로 배열을 한 칸 씩 미는 부분이 있다. 
삽입 정렬에서는 정렬된 배열에서 새로운 원소를 넣기 위해서 하나씩 자리를 밀었다면, 선택 정렬에서는 정렬되지 않은 배열에서 가장 작은 값을 가장 앞으로 가져오게 하려고 자리를 밀었다.

개인적으로 'Binary Insrtion Sort'에서 굳이 위치를 빠르게 찾은 후에, 다시 그 자리에 넣기 위해 배열을 하나씩 미는 행위는 아무리 봐도 조금 합리적이지 못해 보인다...

## 참고

https://www.geeksforgeeks.org/insertion-sort/
