---
title: "Pyinstaller를 이용한 실행파일 만들기"
date: 2021-05-05 19:36:00 +0900
toc: true
toc_sticky: true
tags:
    - tech
    - language
    - python
---

회사에서 python으로 클릭 매크로든 크롤링이든 혼자 재밌는걸 만들다 보면 배포하고 싶어질 때가 생깁니다.

현재 회사가 SW 쪽도 아니고 다들 python을 쓰고 있는 것도 아니라서 `.exe` 혹은 `.bat`로 공유해줘야지 사람들이 쓸 수 있습니다. 이때, 실행파일 만드는 법이 막막할 수 있는데, python 패키지 중 **pyinstaller**로 쉽게 만들 수 있습니다.

## 한 줄 요약

```console
$ pyinstaller --onefile macro.py --hidden-import pywintypes
```

## Pyinstaller 설치

```console
$ pip install pyinstaller
```

## 기본 사용법

아래의 cmd로 `main.py`를 실행 시킬 수 있는 `.exe`파일을 만들어 줍니다.

```console
$ pyinstaller main.py
```

하나의 `.exe`파일을 기대했지만 폴더에는 여러개의 파일들이 만들어지게 됩니다. **dist** 폴더에 가면 `.exe`파일이 있긴 하지만 그밖에도 'dll' 파일이라든가 잡다한게 많습니다. 사내에서 공유 할 때 깔끔하게 하나의 `.exe` 파일만 배포하고 싶으므로 처음 cmd를 약간 수정해서 하나의 파일로 모두 합치게끔 합니다.

```console
$ pyinstaller -F main.py
혹은
$ pyinstaller --onefile main.py
```

위 cmd로 생성된 파일을 확인하면 **dist** 폴더 안에 하나의 `.exe`만 있는 것을 알 수 있습니다.

## 고급 사용법

네, `.exe` 실행해도 바로 꺼지는 경우가 있을 겁니다! 저도 처음에 많이 당황했습니다. 열심히 찾아 본 결과 라이브러리 등의 패키지를 같이 포함 시키지 않았기 때문에 생기는 일이더군요.

`pyinstaller`가 실행파일을 만들게 되면 **dist** 폴더 말고도 **build** 폴더, 그리고 **main.spec**이라는 spec 파일이 있을 겁니다. spec 파일은 `.exe`를 만들기 위해 참고하는 **레시피** 같은 개념으로 보면 됩니다. 여기에서 **hiddenimports** 부분에 사용한 모듈 혹은 패키지들을 전부 넣어 주면 됩니다. 또는 따로 GUI 파일이 있어 `.exe` 실행시킬 때 생기는 콘솔 창을 없애고 싶다? 그러면 아래 `console=True`부분을 `console=False`로만 바꿔 주면 됩니다.

```python
# -*- mode: python ; coding: utf-8 -*-

block_cipher = None


a = Analysis(['main.py'],
             pathex=['C:\\Users\\lazyd],
             binaries=[],
             datas=[],
             hiddenimports=[],
             hookspath=[],
             runtime_hooks=[],
             excludes=[],
             win_no_prefer_redirects=False,
             win_private_assemblies=False,
             cipher=block_cipher,
             noarchive=False)
pyz = PYZ(a.pure, a.zipped_data,
             cipher=block_cipher)
exe = EXE(pyz,
          a.scripts,
          a.binaries,
          a.zipfiles,
          a.datas,
          [],
          name='main',
          debug=False,
          bootloader_ignore_signals=False,
          strip=False,
          upx=True,
          upx_exclude=[],
          runtime_tmpdir=None,
          console=True )
```

이렇게 spec 파일을 잘 조절하면 원하는 .exe 파일로 만들 수 있습니다. 마지막으로 주의 사항은 이 spec 파일을 만들고 나서 다시 `.exe`파일을 만들 때는 반드시 `.spec`파일을 pyinstaller로 불러와야 합니다.

```console
$ pyinstaller --onefile main.spec
```

## 추가 Tip

이건 제가 윈도우 매크로 만들 때 겪은 문제였는데요, `win32gui`, `win32api` 등을 사용했는데 아무리 **hiddenimport**에 넣어도 에러가 발생했습니다. 분명 정상적으로 `.spec` 파일을 만들었는데도 말이죠.

결론은 파이썬에서 `win32`류 라이브러리를 사용할 때는 `pywintypes` 으로 넣어줘야 한다고 합니다. 추가로 spec 파일로 하기 귀찮을 때는 아래처럼 간단하게 `--hidden-import something`해줄 수도 있습니다.

```console
$ pyinstaller --onefile macro.py --hidden-import pywintypes
```
