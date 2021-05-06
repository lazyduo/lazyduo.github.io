---
title: "JUNGOL - 1225 사람감시"
date: 2021-05-06 23:37:00 +0800
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - cpp
---

double 자료형의 사용과 유효숫자를 고려하여 천 분률로 count하는 것이 포인트다. 코딩 문제에서 두점의 거리를 구하거나 반지름의 길이를 구하거나 할 때, 굳이 `sqrt`로 루트를 씌우지 말고, 제곱인 채로 두는 것이 이득이다.

**Tip** double 자료형의 입출력은 `%lf`

- [문제 링크](http://www.jungol.co.kr/bbs/board.php?bo_table=pbank&wr_id=508&sca=99)

```cpp
/**************************************************************
    Result: Success
    Time:24 ms
    Memory:1220 kb
****************************************************************/
 
 
#include <stdio.h>
#include <vector>
 
using namespace std;
#define PI 3.141
 
int cntMax;
 
int divCnt = 1000;
vector<pair<double, double> > point;
 
void check(double x1, double y1, double x2, double y2, double K) {
 
    for (int i = 0; i <= divCnt; i++)
    {
        double K1 = K * i / 1000;
        double K2 = K * (1000 - i) / 1000;
         
 
        int cnt = 0;
        for (auto& x : point)
        {
            double r1_2 = (x1 - x.first) * (x1 - x.first) + (y1 - x.second) * (y1 - x.second);
            double r2_2 = (x2 - x.first) * (x2 - x.first) + (y2 - x.second) * (y2 - x.second);
 
            if (((r1_2 * PI) <= K1) || ((r2_2 * PI) <= K2))
            {
                cnt++;
            }
 
        }
        if (cntMax < cnt)
            cntMax = cnt;
    }
}
 
int main()
{
    // freopen("input.txt", "r", stdin);
 
    int N;
    scanf("%d", &N);
 
    double x1, y1, x2, y2, K;
    scanf("%lf %lf %lf %lf %lf", &x1, &y1, &x2, &y2, &K);
 
 
    for (int i = 0; i < N; i++)
    {
        double X, Y;
        scanf("%lf %lf", &X, &Y);

        point.emplace_back(X, Y);
    }
 
    check(x1, y1, x2, y2, K);
 
    printf("%d", N - cntMax);
    return 1;
 
}
```