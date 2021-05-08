---
title: "PROGRAMMERS - 사칙연산"
date: 2021-05-08 23:01:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - cpp
    - DP
---

**동적 계획법(Dynamic Programming)** 문제. DP는 항상 풀이 설계하는데 많은 어려움을 겪는거 같다. 무엇을 어떻게 `Memoization` 시킬 것인가는 정말 많은 문제를 풀어보는 방법 밖에 없는 것 같다.

이 문제에서는 idx i ~ j 까지의 가능한 연산 값을 최대, 최소 모두 각각 `dp_max`, `dp_min`에 기록해야한다. for 문은 연산의 길이(연산자를 몇개 갖고 있는지)를 늘려가면서 i ~ j 을 `dp` 배열에 입력시키고, 연산자가 '+'인지, '-'인지에 따라 `dp_max`, `dp_min`을 갱신하는 수식이 달라짐을 주의하자.

- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/1843)

```cpp

#include <algorithm>
#include <vector>
#include <string>
#include <memory.h>
using namespace std;

int dp_max[101][101];
int dp_min[101][101];

int solution(vector<string> arr)
{
	int answer = 1;
	int num = arr.size() / 2 + 1;
	memset(dp_max, -1010000, 101*101);
	memset(dp_min, 1001000, 101*101);

	for (int i = 0; i < num; i++) {
		dp_max[i][i] = atoi(arr[i * 2].c_str());
		dp_min[i][i] = atoi(arr[i * 2].c_str());
	}

	for (int calc = 1; calc < num; calc++) {
		for (int i = 0; i < num - calc; i++) {
			int j = calc + i;
			for (int k = i; k < j; k++) {
				if (arr[k * 2 + 1] == "-") {
					dp_max[i][j] = max(dp_max[i][k] - dp_min[k + 1][j], dp_max[i][j]);
					dp_min[i][j] = min(dp_min[i][k] - dp_max[k + 1][j], dp_min[i][j]);
				}
				else if (arr[k * 2 + 1] == "+") {
					dp_max[i][j] = max(dp_max[i][k] + dp_max[k + 1][j], dp_max[i][j]);
					dp_min[i][j] = min(dp_min[i][k] + dp_min[k + 1][j], dp_min[i][j]);
				}
			}
		}

	}
	answer = dp_max[0][num - 1];
	return answer;
}

```