---
title: "Visual Studio Code Python 환경설정"
date: 2021-04-31 03:05:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - ETC_Posts
---

TensorFlow 깔고 실행하는데 처음 한 번은 분명 잘 돌아가는데,
그 다음 run 할 때마다 갑자기 `No module named 'tensorflow'`를 시전하시는 우리의 VS Code..

    Traceback (most recent call last):
    File "c:/Users/lazyd/project/lazyduo.github.io/assets/scripts/tf_tutorial.py", line 1, in <module>
        import tensorflow
    ModuleNotFoundError: No module named 'tensorflow'

따로 cmd창 열고 실행시키면 분명 돌아간다. 그런데 대체 왜 VS Code `TERMINAL`은 말썽인걸까? 한 30분 넘게 씨름했다.
결론은 VSCode에 설정된 python interpreter version이랑, 내 컴퓨터에 깔린 최신 python 버전이랑 달라서 생긴일이었다.
예전에 3.8로 설정해놓고 3.9 설치하고 나서 추가로 설정을 안해줘서 그런것..!

## Visual Studio Code 환경 설정
환경 설정을 위해 VS Code에서 `Ctrl + Shift + P` **Command Palette**를 띄운다.

그 다음 **Python: Select Interpreter** 누르고 전체 혹은 부분 workspace에서 설정한거지 선택한 다음에
원하는 python version을 선택하면 끝.

더 세세한 정보는 아래 링크 참고

[Using Python enviroments in VS Code](https://code.visualstudio.com/docs/python/environments)