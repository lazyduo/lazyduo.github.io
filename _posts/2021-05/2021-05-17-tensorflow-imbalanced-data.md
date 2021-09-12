---
title: "불균형 데이터 분류"
date: 2021-05-17 10:58:00 +0900
classes: wide
toc: true
tags:
    - tech
    - AIML
    - tensorflow
---

이진 분류 문제를 푸는데 테스트 케이스들이 전부 너무 낮은 확률이 나온다.

모델의 설정을 다 확인해 보아도 계속 너무 낮게만 나온다. 원인이 뭘까..

'Activation', 'Optimizer', 'Loss function' 전부 건드려봐도 계속 비슷한 결과만 나온다. 구글링을 통해 분류 문제에 적합한 손실 함수 세팅하는 것도 알아냈고, 아무리 생각해도 모델에는 문제가 없어 보여서 원인을 찾기가 너무 힘들었다.

```
// Predict 출력 결과
[[0.14517547]
 [0.16570579]
 [0.16899477]
 ...
 [0.15710646]
 [0.13629885]
 [0.13853809]]
```

모델 설정

```python
import tensorflow as tf
from tensorflow.keras.optimizers import RMSprop

model = tf.keras.models.Sequential([
        tf.keras.layers.Dense(16, activation='relu', input_shape=(887,)),
        tf.keras.layers.Dense(64, activation='relu'),
        tf.keras.layers.Dense(1, activation='sigmoid')
]) 

model.compile(optimizer=RMSprop(learning_rate=0.001),\
        loss='binary_crossentropy',\
        metrics=['accuracy'])
```

## 불균형 데이터 분류

하루 종일 고민하다가, 데이터 셋이 뭔가 이상한거 아닐까? '민감도' 같은게 너무 낮아서 test 데이터의 예측결과 확률이 낮은게 아닐까? 이 확률을 좀 강제로 높여서 0.5 근처로 값을 나타내게 할 수 없을까?(sigmoid) 라는 생각을 했다.

결국 답을 찾았다.

학습한 데이터가 **`imbalamced`**였던 것이다.

```python
import numpy as np

neg, pos = np.bincount(train_y)
total = neg + pos
print('Examples:\n    Total: {}\n    Positive: {} ({:.2f}% of total)\n'.format(
    total, pos, 100 * pos / total))
```

레이블 불균형 확인!!

```
// 출력
Examples:
    Total: 6000
    Positive: 857 (14.28% of total)
```

사실 14% 이 정도가 '불균형'이라고 말 할 수 있는건지 뭔지는 잘 모르겠다. 예시는 0.2% 이 정도 느낌이라.. 여튼 시도 해보자!

## 클래스 가중치 설정

[링크](https://www.tensorflow.org/tutorials/structured_data/imbalanced_data#%ED%81%B4%EB%9E%98%EC%8A%A4_%EA%B0%80%EC%A4%91%EC%B9%98)

우선 가중치를 설정하자.

```python
weight_for_0 = (1 / neg)*(total)/2.0 
weight_for_1 = (1 / pos)*(total)/2.0

class_weight = {0: weight_for_0, 1: weight_for_1}

print('Weight for class 0: {:.2f}'.format(weight_for_0))
print('Weight for class 1: {:.2f}'.format(weight_for_1))
```

아래와 같이 '0'에는 0.58, '1'에는 3.50의 가중치를 새로 부여했다.

```
// 출력
Weight for class 0: 0.58
Weight for class 1: 3.50
```

이렇게 설정한 가중치는 `model.fit()`에서 argument로 추가해주면 된다.

```python
model.fit(train_X, train_y, epochs=10, class_weight=class_weight)
```

## 결과

그 후 예측 결과

```
// 출력
[[0.39990312]
 [0.47534677]
 [0.52598375]
 ...
 [0.45658126]
 [0.41526577]
 [0.45049655]]
```

확실히 '구분' 할 수 있을 정도로 결과가 좋아 졌다. 이제 이 sigmoid 확률 값으로 0.5 이상은 '1', 아래는 '0'으로 주면 분류 끝!

