---
title: "Click Macro 만들기 - 기록 (2)"
date: 2021-05-16 00:50:00 +0900
classes: wide
toc: true
tags:
    - tech
    - ETC
    - ETC_Posts
    - language
    - python
---

기본 기능 연결 완료 했습니다.

[GitHub](https://github.com/lazyduo/win-click-macro)

매크로 시작 / 중지 기능을 구현하기 위해 python의 `threading` 기본 라이브러리를 사용했습니다. thread 돌아가는 중에 버튼 입력으로 `whilde`문을 멈추는 것이 관건 이었는데, `threading.Event()` 객체 활용하여 처리 했습니다. 현재 모습은 아래와 같습니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/click-macro-2.png){: .align-center}

## 완료 기능

- 현재 활성화 된 창에서 원하는 창 선택 가능

- 마우스 클릭할 위치 설정 가능

- 클릭 주기 설정

- thread를 통한 시작 / 중지 기능 **(추가)**

- X / Y Slider Position 입력 기능 **(추가)**

## 추가할 기능

- step 설정 : click / double-click / type / enter / pause 스텝을 추가해서 일련의 sequence로 매크로를 돌리는 기능

## Threading 처리 모습

[`Event`](https://docs.python.org/3/library/threading.html#event-objects) 활용

```python
import threading

class Ui(QtWidgets.QMainWindow):
    def __init__(self):
        self.stop_event = threading.Event()

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

            if self.stop_event.wait(timeout = self.time_interval):
                print("macro is stopped...")
                self.stop_event.clear()
                return

```