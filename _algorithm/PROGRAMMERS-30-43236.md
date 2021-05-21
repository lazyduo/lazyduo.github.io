---
title: "PROGRAMMERS - 징검다리"
date: 2021-05-20 22:53:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - cpp
    - Binary Search
---

`이분탐색(Binary Search)` 문제. 일단 이 문제는 Binary Search 카테고리 힌트가 없었다면, 풀지 못했을 것 같다.

'0'과 'distance' 사이의 어떤 값(mid)이 원하는 정답이라고 생각하고 찾아나간다. 제거하는 바위의 숫자가 'n'보다 크다면, 다시 기존의 'mid' 값 보다 작은 범위에서 새로 'mid' 값을 찾아서 탐색한다.

반복 과정에서 제거한 바위의 숫자가 'n'보다 작거나 같다면, 이번에는 'mid'보다 큰 범위에서 새로 'mid' 값을 찾으며, 답에 기존 mid 값을 갱신힌다.

(무조건 n이랑 같은 경우가 생기고, 이 때가 찾고자 하는 답이므로 n과 같을 때만 답을 갱신해도 될 것 같다.)

머리를 좀 써야한다. 위의 방법으로 `Binary Search` 했을 때 찾고자하는 답이 나온다는 걸 깨닫는데 좀 시간이 걸렸다...

**Tip** 문제 접근을 다양한 각도에서!

- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43236)

```cpp
#include <vector>
#include <algorithm>


using namespace std;

int solution(int distance, vector<int> rocks, int n) {
    int answer = 0;
    sort(rocks.begin(), rocks.end());
    rocks.emplace_back(distance); // 마지막 바위도 체크하기 위함
    
    int left = 0;
    int right = distance;
    int mid; // 확인하려는 거리 최소값
    
    while (left <= right){
        mid = (left + right) / 2;
        
        int prev = 0;
        int removeRockCnt = 0;
        for (int curr : rocks) {
            if (curr - prev < mid) // 거리 최소값보다 작을 경우 제거 필요
                removeRockCnt ++;
            else {
                prev = curr;
            }
        }
        
        if (removeRockCnt > n) // 제거한 횟수가 n보다 커서 실패
            right = mid - 1;
        else {
            left = mid + 1;
            answer = mid; // 제거가 성공하여 갱신할 경우 answer 업데이트
        }        
    }
    
    return answer;
}
```