---
title: "Python Shorcuts"
date: 2021-09-08 14:55:00 +0900
classes: wide
toc: true
tags:
    - tech
    - language
    - python
---

python을 pythonic하게 쓰는 방법들.

original : [Tech With Tim](https://www.youtube.com/watch?v=CssrFJGH_dU)

## F string

`f'blahblah {variable}'`!! 지금까지 print("%d" %variable) 형태로 써왔다면 파이썬에서는 이제 이렇게 쓰자!

혹은 `'blahblah {}'.format(variable)` 도 좋다.

```python
name = "Dada"

print(f'My name is {name})
```

## Unpacking

enumerate 함수를 for 문에서 돌릴 때 자연스럽게 사용했던 방법이다.

```python
L = (1,2,3)

a, b, c = L

for idx, element in enumerate(L):
    print(idx, element)
```

## Multiple Assignment

swap 하기 위해 temp 를 안써도 되는 놀라운 마술.

```python
a, b = 2, 3

a, b = b, a
```

## Comprehensions

배열 init할 때 정말 쉽게 해주는 기법.

```python
x = [[0 for _ in range(5)] for _ in range(5)]
y = [i for i in range(5)]
```

## Object Multiplication

```python
x = [] * 5
y = 'hello' * 3
```

## Inline / Ternary Condition

python에서는 `x = 1 if 2 > 3 else 0`와 같은 삼항 연산자는 없다. 대신 비슷하게 아래와 같이 쓸 수 있다.

```python
x = 1 if 2 > 3 else 0
```

## Zip

```python
names = ['tim', 'joe', 'billy']
ages = [23, 32, 25]
eye_color = ['blue', 'brown', 'black']

print(list(zip(names, ages, eye_color)))
```

## *args, **kwargs

*, ** 의 차이를 잘 이해하자. 보통은 kwargs 혹은 args 라는 이름도 똑같이 해서 넘기긴 하는데 변수명으로 다른 이름이 들어가도 상관 없다. 실체는 '*' 이니까..

```python
def func1(arg1, arg2, arg3):
    print(arg1, arg2, arg3)

def func2(arg1=None, arg2=None, arg3=Nxone):
    print(arg1, arg2, arg3)

args = [1, 2, 3]
kwargs = {'arg2':2, 'arg1':1, 'arg3':3}

func1(args)
func1(*args)
func2(*kwargs)
func2(**kwargs)
```

## For Else & While Else

아래 경우 처럼 for 문이나 while 문으로 특정 배열에서 무언가를 찾고, 특정 조건을 만족했는지 확인하고 확인 되었다면 A, 확인이 안되었다면 B 하는 경우가 많을 것이다. 보통 (나도 그랬다) flag를 세워서 조건에 만족하면 flag를 True로 만들고 break, 그 후 빠져나온 루프에서 flag 여부에 따라 A 또는 B 실행하는 식으로 코딩을 했을 것이다. 하지만! 아래처럼 For Else, While Else로 쉽게 가능하다. 

```python
for element in search:
    if element == target:
        print('I found it!')
        break
else:
    print('I didn\'t find it!')
```

## Sort By Key

이건 정말 많이 쓰이는 기법으로 Sort 뿐만 아니라 map에서도 많이 사용 된다. 제 블로그 글로 대신 합니다.

[글 보러가기](https://lazyduo.github.io/my-py-tip/#lambda-%ED%95%A8%EC%88%98%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-map%EA%B3%BC-sort)

## Itertools

우선 list와 iterator의 차이를 확실히 알아야 한다.

list는 배열 선언으로 메모리를 많이 먹는 단점이 있지만, 특정 위치의 값을 indexing 할 수 있다. iterator는 반대로 메모리는 효율적이나 중간 순서의 값에 대한 확인이 불가능 하다. 무조건 순서대로만 확인 가능하다.

따라서 용도에 따라 iterator를 쓰는 것이 더 효과 적인 코딩이 될 수 있다.

```
>>> L = [i for i in range(100)]
>>> sys.getsizeof(L)
920
>>> l = iter(L)
>>> sys.getsizeof(l)
48
```

- itertools tip

```python
import itertools

lst = [1, 2, 3, 4, 5]
sum_list = itertools.accumulate(lst)
print(list(sum_list))
#  출력 : [1, 3, 6, 10, 15]

lst2 = ['A', 'B', 'C', 'D']
chain_list = itertools.chain(lst, lst2)
print(list(chain_list))
# 출력 : [1, 2, 3, 4, 5, 'A', 'B', 'C', 'D']
```

