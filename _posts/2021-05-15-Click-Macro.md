---
title: "Click Macro 만들기 - 기록 (1)"
date: 2021-05-15 02:23:00 +0900
classes: wide
toc: true
tags:
    - tech
    - ETC
    - ETC_Posts
    - python
---

Python으로 클릭 매크로를 만들어 보기로 했습니다.

[GitHub](https://github.com/lazyduo/win-click-macro)

처음에는 회사에서 안전교육 동영상을 쉽게(?) 넘기기 위해 만들기 시작했던 매크로 입니다. GUI까지도 생각 안했고, 그냥 하드 코딩으로 마우스 찍고, 엔터 찍는 과정이었는데 조금 더 '제대로'(?) 만들어 보고 싶다는 생각에 이리저리 만들어 보았네요. 하다 보니 생각 만큼 잘 되지는 않네요. 그리고 역시나 하다 보니 계속 욕심이 붙습니다. 이 기능, 저 기능 다 추가해보고 싶어져서 끝이 없을지도 모르겠네요.

PyQt (Qt Designer)로 구현 시킨 모습은 아래와 같습니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/click-macro.png){: .align-center}

## 완료 기능

- 현재 활성화 된 창에서 원하는 창 선택 가능

- 마우스 클릭할 위치 설정 가능

- 클릭 주기 설정

## 추가할 기능

- thread : 현재는 그냥 5회 반복만 해 둠. 시작 / 중지 하기 위해서는 thread 처리를 해야 함.

- step 설정 : click / double-click / type / enter / pause 스텝을 추가해서 일련의 sequence로 매크로를 돌리는 기능

## window control

`pypiwin32`에서 **win32api**, **win32gui**, **win32con** 사용

hwnd를 이용하여 핸들을 가져오게 되므로 이를 id로 해서 다루는게 중요

- 현재 활성 중인 윈도우 핸들(hwnd) 가져오기

    ```python
    import win32gui
    hwnd = win32gui.GetActiveWindow()
    ```

- cursor Position (절대 위치)

    ```python
    import win32api
    pos = win32api.GetCursorPos() # (x,y) tuple 반환
    win32api.SetCursorPos(pos)
    ```
- 창 크기 구하기

    ```python
    import win32gui
    (left, top, right, bottom) = win32gui.GetWindowRect(hwnd)
    ```
- 창을 가장 앞 화면으로 가져오기

    ```python
    import win32gui
    import win32con
    win32gui.ShowWindow(hwnd, win32con.SW_RESTORE)
    win32gui.SetForegroundWindow(hwnd)
    ```


## PyQt ui 연결

오랜만에 해서 굉장히 애를 먹었다.

`uic.loadUi(custom.ui, self)`로 class instance에 만든 ui를 상속시키는게 포인트다.

**Widget**의 이벤트 처리는 'signals' 속성에 `.connect()`해서 함수로 연결해주면 된다. 이 때, 위젯 이름과 시그널 이름, 속성 이름 등은 신경 써서 적어주어야 한다.. 대소문자 유의하자.

[documents](https://doc.qt.io/qt-5/qlistwidgetitem.html)

```python
from PyQt5 import QtWidgets, uic

class Ui(QtWidgets.QMainWindow):
    def __init__(self, **kwargs):
        super(Ui, self).__init__()
        self.ui_name = kwargs.get('name', None)

        # load custom gui
        self.path = os.path.join(
            os.path.dirname(os.path.realpath(__file__)), self.ui_name)
        uic.loadUi(self.path, self)

        # widget handle
        self.listWidget_1.itemDoubleClicked.connect(self.set_window_list)
        self.pushButton_3.clicked.connect(self.run_macro)
        self.pushButton_5.clicked.connect(self.refresh_list)
        self.horizontalSlider_2.valueChanged.connect(self.set_x)
        self.verticalSlider.valueChanged.connect(self.set_y)
        self.horizontalSlider.valueChanged.connect(self.set_time_interval)
        self.pushButton_6.clicked.connect(self.test_position)

        self.show()
```