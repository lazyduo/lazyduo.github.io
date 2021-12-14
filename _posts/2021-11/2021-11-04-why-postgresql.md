---
title: "PostgreSQL Usage "
date: 2021-11-04 21:44:00 +0900
classes: wide
tags:
    - tech
    - computer
    - database
    - postgres
---

인터뷰 때 왜 `PostgreSQL`을 쓰냐는 질문을 많이 받았다.

그때의 할 수 있는 최선의 답변은 '오픈소스라서요...'가 한계였다.

## MySQL vs PostgreSQL

결론 부터 말하면 `PostgreSQL`은 Object-Relational database인 반면에, `MySQL`은 순수한 Relational Database이다. 즉, `Postgres`은 Table Inheritance, Function Overloading 등의 'OOP'에서 할 수 있는 특징들을 가능하게끔 한다. 그러면서도 `Postgres`는 SQL standard를 준수하고 있다.

`PostgreSQL`은 `MySQL`에 비해 아래의 이유들로 동시성(concurrency)을 더 잘 처리한다.

Postgres는 read lock 없이 'Multiversion Concurrency Control(MVCC)'를 구현하고, CPU/core를 사용할 수 있는 병렬 쿼리 계획을 지원한다. 또한 Postgres는 non-blocking 방식으로 인덱스를 생성할 수 있으며(CREATE INDEX CONCURRENTLY 구문) 부분 인덱스를 생성할 수 있다. 예를 들어 일시 삭제가 있는 모델의 경우 삭제된 것으로 표시된 레코드를 무시하는 인덱스를 만들 수 있다. Postgres는 트랜잭션(Transaction) 수준에서 데이터 무결성을 보호하는 것으로 알려져 있어 데이터 손상(corruption)에 덜 취약하다.

## pgAdmin

postgres desktop app.

SSH Server 연결하기.

- Connection
    실제 서버에서의 세팅값으로 가져가면 된다. localhost, 서버의 postgres 계정 접속 정보를 입력한다.

- SSH Tunnel
    타겟 서버를 등록하면 된다. Tunnel Host에는 타겟 ip 주소, 접속하고자 하는 계정 이름과 비밀번호를 세팅한다. 보통 22 port로 외부로 열려 있으니 port는 22로 그대로 두면 된다.
