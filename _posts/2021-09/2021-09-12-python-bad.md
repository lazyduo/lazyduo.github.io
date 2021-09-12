---
title: "Python Bad Practices to Avoid"
date: 2021-09-12 22:25:00 +0900
classes: wide
toc: true
tags:
    - tech
    - language
    - python
---

내가 왜 이걸 이제 알았을까. 코딩 테스트하면서 불편했던 부분들을 싹싹 긁어 주는 꿀 팁.

original : [Tech With Tim](https://www.youtube.com/watch?v=5Ui37whUDrM&t=915)

실제로 이번 주말에 3번의 코딩 테스트(LINE, 카카오, NEXON) 보면서 정말 날 당황하게 했던.. python 이라서 껄끄러웠던 문제들이다..

## Mutable Default Parameter

아래 코드를 살펴보자. 언뜻보면 처음 x 는 'numbers'에 1만 들어갔으니 \[1\], y는 \[1, 2\], z는 \[1, 2, 3\] 일 것 같다. 하지만, 'append_number' 함수에서 return 되는 numbers는 리스트의 주소값으로 참조하기 때문에, 이후의 함수들이 이전 값에 전부 영향을 준다.

따라서, 결국 x, y, z는 전부 \[1, 2, 3\] 이 되어 버린다..

이를 피하기 위해서는 전에 다루었던 [리스트 카피](https://lazyduo.github.io/my-py-tip/#list-copy-%EC%A3%BC%EC%9D%98-%EC%82%AC%ED%95%AD) 문제를 이해하고 사용해야 한다.

```python
def append_number(num, numbers=[]):
    numbers.append(num)
    print(num)
    print(numbers)
    return numbers

x = append_number(1)
y = append_number(2)
z = append_number(3)
print(x is y and y is z)
```

## Default Dictionary

문제를 풀다 보면, 비어 있는 딕셔너리를 정의하고 해당 key가 있으면 그 값에 count 같은거를 더하고, 없으면 해당 key로 하는 아이템을 생성해서 넣어야하는 경우가 있다.

```python
count = defaultdict(lambda: 0)
numbers = [1, 2, 3, 1, 2, 2, 3, 4, 5]
for number in numbers:
    if count.get(number):
        count[number] += 1
    else:
        count[number] = 1
```

그런 경우 나는 계속 위 처럼 `if dicA.get('key'):` 로 검사해서 있으면 '+=', 없으면 '='으로 딕셔너리를 다뤘다. key가 없다면 count\[number\] 이런식의 인덱싱은 에러가 나기 때문이다. 하지만 그럴 필요가 없었다.

- 방법 1 :  defaultdict

defaultdict은 키가 생성 될 때 지정해준 함수로 세팅을 해준다. `defaultdict`의 사용 자체는 원래의 딕셔너리랑 거의 같지만, print시 리턴되는 모습이나. 약간의 사용방법이 다른게 있어서 쓰다가 불편함을 느낄수도 있다. 그러니 나는 방법 2를 사용하겠다..

```python
from collections import defaultdict

count = defaultdict(lambda: 0)
numbers = [1, 2, 3, 1, 2, 2, 3, 4, 5]
for number in numbers:
    count[number] += 1
```

- 방법 2 : setdefault()

신세계. 진짜 정말 아래와 같이 코드하는 경우가 많았는데, 한 줄로 해결 가능하다.

key가 있다면 해당 value를 반환하고, 만약 key가 없다면 입력한 인자로 default 값을 넣어주고, 그 값을 반환한다. (굉장히 멋지다...)

```python
d = {}

if 'list' not in d:
    d['list'] = []

d['list'].append(3)

# setdefault!!
d.setdefault('list', []).append(3)
```

## with open

그냥 open을 쓰면 꼭 'f.close()'로 닫아줘야하는데 `with open`으로 열면 그럴 필요 없다.

## enumerate

이건 알고 있던 내용인데, for문에서 index와 value 값을 동시에 쓰고 싶을 때 한줄이라도 줄이기 위해서 쓴다. 또한 'range(len(L))'을 안써서 좋다.

```python
L = [2, 3, 4, 1, 2, 5, 6]
for idx in range(len(L)):
    val = L[idx]
    print(val)

# enumerate
for idx, val in enumerate(L):
    print(idx, val)
```