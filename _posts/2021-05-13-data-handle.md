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

- dataframe을 numpy로 변환 및 원하는 shape로 바꾸는 방법

    ```python
    X = df.to_numpy().reshape(-1,1)
    ```

## train / test split

주어진 `data`에서 train / test 용 data를 split 하는 방법

```python
from sklearn.model_selection import train_test_split

train_set, test_set = train_test_split(data, test_size=0.2, random_state=42)
```
