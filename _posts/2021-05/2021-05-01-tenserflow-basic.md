---
title: "TensorFlow Tutorial (2) - Beginner"
date: 2021-05-01 06:11:00 +0900
classes: wide
toc: true
toc_sticky: true
tags:
    - tech
    - AIML
    - tensorflow
    - tutorial
---

가장 기본 튜토리얼. 아직 머신러닝 공부가 부족하여 손실 함수 등 이해가 필요한 부분이 많다. 그래도 무언가 훈련하고, 답을 찾아내는게 보여서 신기하다.

[Python Script](https://github.com/lazyduo/tensorflow-tutorial/blob/master/scripts/tf_tutorial.py)

## Data Load

사용할 데이터는 `MNIST`. 숫자 손글씨 Database로, training set 60,000개, test set 10,000개로 이루어져 있다. tensorflow의 keras에 datasets으로 있어서 아래와 같이 불러 올 수 있다. dataset을 로딩하면 NumPy array로 리턴하며, 값 확인을 위해 ndarray.shape로 dimension을 확인 해 보았다.

```python
import tensorflow as tf

mnist = tf.keras.datasets.mnist # dataset load

(x_train, y_train), (x_test, y_test) = mnist.load_data()

print('x_train: ' + str(x_train.shape)) 
print('y_train: ' + str(y_train.shape)) 
print('x_test:  '  + str(x_test.shape)) 
print('y_test:  '  + str(y_test.shape)) 
```

- 출력값

```console
    x_train: (60000, 28, 28) // input training set shape
    y_train: (60000,)        // output training set shape
    x_test:  (10000, 28, 28) // input test set shape
    y_test:  (10000,)        // output test set shape
```

위와 같이 x_train에는 28 x 28 pixel 크기의 이미지가 들어가 있는 것을 볼 수 있다. 각 픽셀에 흑백 명암 정도를 0~255의 정수로 표현되어 있다. 또한 y_train에는 이 이미지가 숫자 1인지 8인지 라벨값(0~9)가 들어가 있다. plot 하여 이미지 확인을 해 보자.

```python
from matplotlib import pyplot

pyplot.figure(figsize=(7,7))
for i in range(25):
  pyplot.subplot(5, 5, i+1)
  pyplot.xticks([])
  pyplot.yticks([])
  pyplot.grid(False)
  pyplot.imshow(x_train[i], cmap=pyplot.get_cmap('gray'))
  pyplot.xlabel(y_train[i])
pyplot.show()
```

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/MNIST.png){: .align-center}
(뭔가 멋있다..)


## Model

예시로 `tf.keras.Squential` 모델을 만들어 보자. 먼저, 레이어를 차례로 쌓아 model을 생성한다.

(명암도를 0~1사이의 값으로 만들기 위해 각 값을 255.0으로 먼저 나누어 주었다.)

```python
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(input_shape=(28, 28)),
  tf.keras.layers.Dense(128, activation='relu'),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10, activation='softmax')
])
```

모델을 출력해보면 "[logits](https://developers.google.com/machine-learning/glossary#logits)" 관련 값들을 확인 할 수 있는데,

```python
predictions = model(x_train[:1]).numpy()
```

`tf.nn.softmax` 함수는 이 logits를 "가능성"으로 전환해준다. 

- 출력값

```console
    [[0.04500094 0.11489239 0.11621773 0.15878086 0.07192232 0.07576974
    0.05411552 0.17347248 0.06605321 0.12377478]]
    ---------
    [[0.0945651  0.10141084 0.10154533 0.10596072 0.09714551 0.09751998
    0.09543097 0.10752894 0.09657701 0.10231561]]
```

이제, 훈련에 사용할 **optimizer**와 **loss** 손실 함수를 선택해야한다. 손실 함수는 `losses.SparseCategoricalCrossentropy`로 할 것이다. (아직 beginner니까 일단 넘어가자)

```python
loss_fn = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True)
```

마지막으로 선택한 optimizer와 loss fn으로 compile 시킨다.

```python
model.compile(optimizer='adam',
              loss=loss_fn,
              metrics=['accuracy'])
```

## Training and Evaluate

`Model.fit` method로 훈련 시킨다.

```python
model.fit(x_train, y_train, epochs=5)
```

- 출력값

```console
    Epoch 1/5
    1875/1875 [==============================] - 5s 2ms/step - loss: 0.2937 - accuracy: 0.9149
    Epoch 2/5
    1875/1875 [==============================] - 4s 2ms/step - loss: 0.1425 - accuracy: 0.9571
    Epoch 3/5
    1875/1875 [==============================] - 4s 2ms/step - loss: 0.1081 - accuracy: 0.9666
    Epoch 4/5
    1875/1875 [==============================] - 4s 2ms/step - loss: 0.0884 - accuracy: 0.9727
    Epoch 5/5
    1875/1875 [==============================] - 4s 2ms/step - loss: 0.0766 - accuracy: 0.9764    
```

`Model.evaluate` model을 "Test-set"과 비교하여 검증한다. fitting 전 후를 비교하면 확실히 차이가 보인다. 약 98%의 정확도를 갖는다.

```python
model.evaluate(x_test,  y_test, verbose=2)
```

- 출력값

```console
    before fitting
    313/313 - 1s - loss: 2.4270 - accuracy: 0.0656
    [2.4269537925720215, 0.06560000032186508]

    after fitting
    313/313 - 1s - loss: 0.0744 - accuracy: 0.9775
    [0.07440521568059921, 0.9775000214576721]
```

## Probability Model

가능성 모델은 훈련된 모델에 softmax layer을 붙여서 모델링하여 만들 수 있다.

```python
probability_model = tf.keras.Sequential([
  model,
  tf.keras.layers.Softmax()
])
```

## 참고
- [머신러닝 용어집](https://developers.google.com/machine-learning/glossary)