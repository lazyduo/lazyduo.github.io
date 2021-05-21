---
title: "PROGRAMMERS - 호텔 방 배정"
date: 2021-05-20 22:46:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - cpp
    - Union-Find
    - Disjoint-set
---

`Union-Find` or `Disjoint-set` 문제. 이 알고리즘을 쓰지 않으면 빈 방을 찾는 과정에서 시간 복잡도가 증가하여 효율성 테스트를 통과할 수 없다.

처음엔 `Union-Find` 라는 알고리즘을 몰랐어서 효율성 부분이 통과가 안되어서 애를 많이 먹었다. 얼핏 생각했을 때는 그냥 'K'만큼의 배열을 만들어서 값이 있는지 없는지 체크하면서 다음 빈 방을 찾으면 될 것 같은데, 문제는 'K'가 10^12로 너무 크다. 따라서 아래의 `Union` 함수 처럼, 다음 빈 방을 각 방마다 매핑해서 쓰지 않으면 시간 복잡도가 해결되지 않는다.

**Tip** 크기 K인 배열에서 계속 ++ 하면서 찾는 생각은 버리자!

- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64063)

```cpp
#include <vector>
#include <map>
typedef long long ll;
using namespace std;

map<long long, long long> room;

ll Find(ll num) {
	if (room.find(num) == room.end()){
        return num;
    }
    return room[num] = Find(room[num]);
}

void Union(ll x, ll y){
    x = Find(x);
    y = Find(y);
    room[x] = y;
}


vector<long long> solution(long long k, vector<long long> room_number) {
    vector<long long> answer;
	
	for (auto num : room_number) {
		ll empty = Find(num);
		answer.emplace_back(empty);
        Union(empty, empty+1);
	}

	return answer;
}
```