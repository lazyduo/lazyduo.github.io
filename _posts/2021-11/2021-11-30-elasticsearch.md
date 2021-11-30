---
title: "Elasticsearch - Tutorial"
date: 2021-11-30 15:21:00 +0900
classes: wide
toc: true
tags:
    - tech
    - AIML
    - elasticsearch
---

어디다 넣어야할지 모르겠으나.. 일단은 머신러닝 카테고리로 넣음.

## Elasticsearch?

## Python Elasticsearch Client

[Document Link](https://elasticsearch-py.readthedocs.io/en/v8.0.0a1/index.html)

username, password 가 설정되어 있다면 꼭 'username:password@'를 url 앞에 붙이자.

```python
from elasticsearch import Elasticsearch
from elasticsearch import helpers

es = Elasticsearch('http://elastic:changeme@localhost:9200')
es.info()
```

- 특정 index 내 모든 항목 삭제

```python
es.delete_by_query(index=index_name, body={'query': {'match_all': {}}})
```