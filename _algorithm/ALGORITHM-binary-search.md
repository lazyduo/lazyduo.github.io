---
title: "ALGORITHM - Binary Search"
date: 2021-09-08 10:26:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
    - search
    - binary search
---

'Search' 알고리즘의 기본. `Binary Search`

##  Intro

사실 모든 알고리즘의 기본일지도 모른다. 코딩 처음 배울 때 거의 필수적으로 얘 부터 배우니 말이다..

우선 '탐색(Search)'은 주어진 배열(array)에서 특정 원소(element)의 위치를 찾는 알고리즘이라고 정의할 수 있고, 가장 기초적인 접근 법은 모든 배열의 원소를 하나 하나 순차적으로 확인하는 'Linear Search'가 있다. 이 'Linear Search'는 최악의 경우 배열의 끝까지 탐색할 수도 있기 때문에 배열의 크기에 비례한 O(N)의 복잡도를 가진다.

이제 `Binary Search`는 탐색할 때 중간 인덱스의 값을 비교하여 절반씩 잘라서 탐색하는 방법으로, 한 번의 interval에 절반을 제거하게 되므로 O(logN)의 복잡도를 갖게 된다. 단, 이때 배열은 반드시 정렬되어 있어야 한다.

## Procedure

1. 찾으려는 원소 x 와 배열의 가운데 원소(middle element)와 비교를 한다.
2. If x 와 가운데 원소가 일치하면 mid index를 리턴한다.
3. Else If x가 가운데 원소보다 크다면, x가 가운데 원소의 오른쪽 부분배열에 위치하므로, 오른쪽 부분 배열에서 알고리즘을 반복한다.
4. Else x 가 작으면 왼쪽 배열에서 알고리즘을 반복한다.

## Code Reference

[source](https://github.com/lazyduo/algorithms-python/blob/main/search/binary_search.py)

두 가지 방법이 있다. recursive 는 함수의 콜백으로 stack overflow 문제가 있을 수 있으니 되도록이면 지양하자. iterative 하게 하도록 노력!

- Recursive

```python
def binarySearch_recur (arr, start, end, x):
    if start <= end:
        mid = start + (end - start) // 2

        if arr[mid] == x:
            return mid
        
        elif arr[mid] > x:
            return binarySearch_recur(arr, start, mid-1, x)

        else:
            return binarySearch_recur(arr, mid + 1 , end, x)
            
    else:
        return -1
```

- Iterative

```python
def binarySearch_iter(arr, start, end, x):
    while (start <= end):
        mid = start + (end - start) // 2

        if arr[mid] == x:
            return mid
        
        elif arr[mid] < x:
            start = mid + 1

        else:
            end = mid -1

    return -1
```

## Note

mid index를 찾는 과정에서 아래와 같이 단순하게
```
mid = (start + end) // 2
```
하지 않고,

```
mid = start + (end - start) // 2
```
를 하는데는 이유가 있다.

바로 start + end 값이 너무 커져 버리면 (ex 4바이트 int의 최대 값인 2^31 - 1) 음수를 반환 할 수 있기 때문이다.

python은 알아서 어느 정도 자동으로 타입을 맞춰 주긴 하지만, 타입이 있는 언어를 사용할 경우 주의가 필요하겠다.

## 참고

geeksforgeeks.org/binary-search/