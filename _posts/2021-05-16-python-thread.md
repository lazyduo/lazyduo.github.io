---
title: "Threading Library"
date: 2021-05-16 01:05:00 +0900
classes: wide
toc: true
tags:
    - tech
    - language
    - python
---

python 기본 라이브러리 `Threading`을 통한 간단한 **thread** 사용 방법 정리.

## Thread?

하나의 프로세스가 하나의 작업만을 처리한다면, 그 작업이 진행하는 동안 우리는 아무것도 못 할 것이다.

프로세스는 `thread` 라는 일꾼(?)들을 갖고 있는 container라고 볼 수 있다. 코딩을 하고 run 했을 때 프로세스는 스크립트를 읽으면서 명령을 실행하게 되는데, 이 때 실행의 주체가 `thread` 이다. 무한 while 문을 돌고 있을 때 다른 동작을 할 수 없듯이 하나의 `thread`는 하나의 명령만을 실행한다.

따라서, 어떤 프로그램이 자동으로 뭔가 계속 업데이트 하고 있는 와중에 무언가 동작을 시킬려면 `thread` 분리 없이는 둘 중에 하나는 실행 시키지 못한다.

즉, 컴퓨터 한테 잔뜩 동시 다발적으로 일을 시키고 싶다면 `threading`을 하란 소리다.

## python threading library

python에서는 기본 라이브러리로 `threading`을 제공한다.

아래는 `Thread` 객체 생성 방법이다.

```python
import threading

class threading.Thread(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)
```

이 때 `daemon`이란 개념은 프로세스가 종료 될 때 같이 종료 되는 `thread`를 의미한다. 예를 들어 run.py를 돌렸는데, 다른 `thread`에서 작업 중인 와중에 run.py를 꺼버리면 해당 `thread`도 종료 된다.

기본적으로 아래와 같이 세팅해서 사용한다고 보면 된다.

```python
import threading

def funcThread(x, y)
    # do something whit x, y
    return

x = 1
y = 2

t = threading.Thread(target=funcThread, daemon=True, args=(x,y))
t.start()

```


## 활용 예시

`threading.Event()`를 이용하여 `thread`가 돌고 있는 중간에 `Event.wait()` 메소드로 thread를 강제 종료 시키는 방법이다.

(Event 객체는 set()으로 동작 여부를 internal flag를 다룰 수 있게 해주기 때문에 이러한 방식으로 쓰인다)

[threading docs](https://docs.python.org/3/library/threading.html)

```python
import threading

class Ui(QtWidgets.QMainWindow):
    def __init__(self):
        self.stop_event = threading.Event() # Event 객체 생성

    def run_macro(self):
        context ={'name': self.selected_window_name, 'hwnd': self.selected_window_hwnd}
        self.macroThread = threading.Thread(target=self.runMacro, daemon=True, kwargs=context)
        self.macroThread.start()

    def stopMacro(self):
        self.stop_event.set()

    def runMacro(self, **kwargs):
        self.macro = Window(**kwargs)

        while True:
            self.macro.set_foreground_window()
            self.macro.click_target_window((self.x_ratio, self.y_ratio))

            if self.stop_event.wait(timeout = self.time_interval): # Event.wait
                print("macro is stopped...")
                self.stop_event.clear()
                return

```