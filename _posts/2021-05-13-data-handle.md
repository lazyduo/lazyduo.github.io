---
title: "Data Handling for ML"
date: 2021-05-13 11:34:00 +0900
classes: wide
tags:
    - tech
    - AIML
    - python
---

Data Handling을 위한 개인 메모 포스트 입니다.

## 기본 라이브러리

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import sklearn.linear_model
```

## numpy, pandas

- DataFrame을 numpy로 변환 및 원하는 shape로 바꾸는 방법

    ```python
    X = df.to_numpy().reshape(-1,1)
    ```
    
- `df.head()` : DataFrame class의 처음 5개 행까지의 데이터를 보여준다.
- `df.info()` : 정보 표시 (column의 종류, 타입 등)
- `df["col1"].value_counts()` : col1 이름의 column에서 valu 값들을 count 해준다.
- `df.describe()` : count, mean, std, min, 사분위, max의 요약 통계 정보를 column별로 보여준다.

## train / test split

주어진 `data`에서 train / test 용 data를 split 하는 방법

```python
from sklearn.model_selection import train_test_split

train_set, test_set = train_test_split(data, test_size=0.2, random_state=42)
```
