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

### 기본

- DataFrame 생성 : `pd.DataFrame('dictionary')`
- DataFrame을 numpy로 변환 및 원하는 shape로 바꾸는 방법

    ```python
    X = df.to_numpy().reshape(-1,1)
    ```
- `df.head()` : DataFrame class의 처음 5개 행까지의 데이터를 보여준다.
- `df.info()` : 정보 표시 (column의 종류, 타입 등)
- `df["col1"].value_counts()` : col1 이름의 column에서 valu 값들을 count 해준다.
- `df.describe()` : count, mean, std, min, 사분위, max의 요약 통계 정보를 column별로 보여준다.
- index 순서로 정렬 : `pd.DataFrame(~~).sort_index()`

### 기존 column을 원하는 구간으로 나눠서 새롭게 라벨링하기

`pd.cut()` method를 사용하며, `bins` 에 원하는 구간을 설정하고 `labels`에 원하는 라벨을 새로 설정한다.

```python
df["new"] = pd.cut(df["old"],
                   bins=[0., 2., 4., 6., 8., np.inf],
                   labels=[1, 2, 3, 4, 5])
```

### plot

pandas의 DataFrame은 plot 기능을 제공하며, 아래와 같이 사용한다. `alpha` 값을 주어 밀집 현황도 잘 볼 수 있다.

or `df.plot.scatter(x="", y="")` 도 가능

```python
df.plot(kind="scatter", x="x_name", y="y_name", alpha=0.1)
```

심화 버전

`s` : 원의 size를 의미. 값에 대응 시켜 원의 크기를 조절 할 수 도 있다.
`c` : color-> 어떤 컬럼을 이용해서 색깔 변화를 줄지 선택한다.
`cmap` : 사용할 컬러 맵을 선택한다. 보통 "jet"가 많이 쓰임.

```python
df.plot(kind="scatter", x="x_name", y="y_name", alpha=0.4,
             s=df["col1"]/100, label="This is label", figsize=(10,7),
             c="col2", cmap=plt.get_cmap("jet"), colorbar=True,
             sharex=False)
 ```

## train / test split

주어진 `data`에서 train / test 용 data를 split 하는 방법

'stratify'는 특정 컬럼의 라벨 비율을 유지하면서 test set을 split하는데 사용 된다.

```python
from sklearn.model_selection import train_test_split

train_set, test_set = train_test_split(data, test_size=0.2, random_state=42, stratify=df["target"])
```
