---
title: "PostgreSQL - Study "
date: 2021-12-19 19:24:00 +0900
classes: wide
tags:
    - tech
    - computer
    - database
    - postgres
---

GPU를 사용하는 데이터베이스를 만들자...!!! (회사 일을 위한 스터디)

# PostgreSQL

[참고 링크](https://www.interdb.jp/pg/index.html)

## Background

### Database Layout

각 데이터 베이스틑 base 디렉토리의 서브 디렉토리로 존재.

- **object identifiers (OIDs) - unsigned 4Byte integer : 각 데이터 베이스 오브젝트는 고유의 OID를 갖음.  각 데이터베이스 파일은 1GB를 넘지 않으며 자동 확장 됨.**
- free space map (_fsm)
- visibility map (_vm)
- forks. data file - fork 0, fsm - fork 1, vm - fork 2

Tablespace → version specific subdirectory? database 의 버전을 특정하기 위해서?

![tablespace]({{ site.url }}{{ site.baseurl }}/assets/images/db_image/db-1.png){: .align-center}

### Heap Table File

![heap-table]({{ site.url }}{{ site.baseurl }}/assets/images/db_image/db-2.png){: .align-center}

- heap tuple - record data
- line pointers - heap tuple을 가리키는 포인터, 새로운 레코드가 생기면 새로운 포인터가 생김. 각 번호는 offset number로 불리며 1부터 차례대로 매겨짐.
- Header Data
- Tuple idendifier(TID) → table file의 block number로 해당 페이지, line ponter의 offset number로 해당 튜플을 찾음.
- Writing - pd_lower, pd_upper가 튜플의 처음과 끝 line pointer를 가리킴.

![writing]({{ site.url }}{{ site.baseurl }}/assets/images/db_image/db-3.png){: .align-center}

- Reading
    - Sequential Scan : Index 없이 차례로 모든 페이지(block), heap tuple 검색
    - Index Scan : Index Tuple에 맞는 Key가 있다면 TID(block, offset)으로 바로 힙튜플을 찾아감.

![reading]({{ site.url }}{{ site.baseurl }}/assets/images/db_image/db-4.png){: .align-center}