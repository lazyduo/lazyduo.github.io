---
title: "Hash Table Keywords"
date: 2021-10-23 00:02:00 +0900
classes: wide
tags:
    - tech
    - computer
---

## Keywords
- Key-value O(1)
- Bucket : result of the hash function.
- Collision
    - Two keys result in the same value
    - Collision handling technique
        - Separate Chaining : same key일 경우 링크드 리스트 혹은 트리 등으로 연결하는 방법. 
        - Open Addressing : 같은 테이블 안에서 비어있는 Bucket을 찾는다.
            - Linear Probing : 충돌이 일어날 경우 다음 테이블로 선형적으로 탐색하는 하여 저장하는 방법. 단점으로는 Primary Clustering이 일어난다. 해쉬 충돌이 특정 영역에 집중되기 때문.
            - Quadratic Probing: Linear Probing의 단점을 줄이고자 해쉬 함수를 2차 식으로 만든다. 하지만 Primary Clustering과 마찬가지로 Secondary Clustering 문제가 발생한다.
            - Double Hashing : 위의 단점들을 보완하기 위해서 해쉬 함수를 두개를 사용한다.
        - Separate Chaining vs Open Addressing
            - 구현이 비교적 간단 / search 과정에 계산이 필요함.
            - table이 가득 찰 일이 없음 / 가득 차면 해쉬 테이블을 확장할 필요가 있음.
            - 해쉬 함수에 대해 less sensitive / 해쉬 함수에 따라 clustering에 대한 처리가 필요함
            - 주로 어떤 key들이 어떤 빈도로 들어오는지 잘 모를 때 사용 / 어느 정도 예측 가능한 key일 때 주로 사용
            - Cache performance가 좋지 않음 / 결국 O(1)이기 때문에 Cache performance가 좋음
            - Wastage of Space가 있음. 특정 부분의 해쉬 테이블이 아예 안쓰일 수 있기 때문 / 매핑이 되지 않았던 테이블도 사용되게 됨
            - 연결 리스트로 인한 추가적인 공간이 필요 / 추가적인 공간이 필요 없음.