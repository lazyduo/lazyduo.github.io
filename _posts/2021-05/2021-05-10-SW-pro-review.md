---
title: "삼성 SW 검정 시험 Pro 등급 취득 후기"
date: 2021-05-10 23:11:00 +0900
tags:
    - dairy
    - algorithm
    - cpp
---

Pro 등급 취득하였습니다.

21년 2월 19일 Adv 등급 취득 이후 사내 교육 1주일 받고 바로 취득했네요. 남들은 대여섯 번 치면서 아는 문제 나올 때까지 도전한다고 하던데 운이 좋았던 것 같습니다.

직무 변경 후 틈틈이 C언어로 코딩 테스트 준비하며 도움 없이 Adv을 취득했었는데, Pro 대비반 교육에서는 갑자기 강사가 C++로 시험을 보는 게 좋다고 해서 급하게 C++ 문법과 STL 몇 가지 숙지하고 시험 치렀습니다.

짧은 준비 기간이었음에도 불구하고 Adv, Pro 한 번에 취득할 수 있었던 것은 아무래도 운이 좋았던 것 같습니다.

Adv 때는 사실 뜻대로 잘 안되서 시간 끝까지 쓰다가 막판에 테스트 케이스 통과하여 겨우 붙었고, Pro 시험 때는 문제들에 그래도 좀 익숙해졌는지 Adv보다는 체감상 쉬웠던 것 같습니다. (실제 난이도가 쉬웠던 건지도 모르겠습니다.)

제 Pro 시험 문제는 0과 1로만 된 자물쇠를 돌려가며 한 줄이 모두 1이 되게 하는 최소의 'Click' 수를 찾는 문제였습니다. **완전 탐색**에 적절한 **백트래킹** 조건을 통해 시간을 줄이는 게 관건이었던 것 같습니다. 모든 칸마다 현재의 위치에서 가장 가까운 1의 위치를 찾는 게 핵심으로 저는 C++ STL의 `<algorithm>`에서 **lower_bound**을 이용하여 풀었습니다. 아마 이 알고리즘을 쓰지 않고 풀었다면 O(N^2)으로 시간 초과가 났을 것으로 예상합니다.

`Dijkstra`의 경우도 heap 혹은 우선순위 큐를 사용하지 않으면 O(NlogN)이 안되는 것 처럼 이런 사소한(?) 부분으로 Pro와 Adv 등급을 나누는 것 같습니다.

하여튼 한 번에 취득해서 너무 기분이 좋네요.