---
title: "Flask - Python Web Framework"
date: 2021-07-05 14:32:00 +0900
classes: wide
toc: true
tags:
    - tech
    - language
    - python
    - flask
---

python 웹프레임워크로 'django' 밖에 안써봐서 `flask`도 한 번 써보기로 했습니다.

`flask`는 'django'에 비해 가볍고 (단점일수도), 쉽게 시작할 수 있는 장점이 있습니다.

직접 써보니 확실히 굉장히 간단하게 웹페이지를 만들 수 있었습니다. 처음 시작하는 입장에서는 확실히 `flask`가 좋아보입니다.

## install

대부분의 python 패키지와 마찬가지로 `pip install falsk`로 쉽게 설치 가능합니다.

버전 꼬일 일 등을 미연에 방지하기 위해 가상환경 venv에서 설치를 권장합니다.

```cmd
(venv) C:\Users\Administrator\Documents\myproject\flask>pip install flask
```

## first step

폴더에 'app.py'를 아래와 같이 생성합니다.

우선 main 실행은 'app.run(debug=True)'으로 app.py를 실행시키면 server를 run 시켜 줍니다. 이 때, 'debug=True' 옵션은 'app.py'가 수정이 일어날 때 바로바로 반영 시켜서 보여주게끔 합니다. 테스트 용으로는 웬만해서는 'debug=True' 해주면 될 것 같습니다.

`@app.route('/')`는 Flask class에서 준비된 함수가 트리거 되어 URL을 rendering 할 수 있도록 하는 decorator이다.

아래와 같이 기본 url에서 'Hello World'를 출력할 수 있게 끔 한다. 이 때 반드시 '/'로 시작해야하는 것을 주의 하자.

url로 부터 변수를 사용하고 싶으면 아래 쪽의 `@app.route('/user/<user_name>/<int:user_id>')` 예시 처럼 사용하면 된다.

'/user/dada/30'에서 'Hello, dada(30)!'을 출력할 것이다.

- app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello World'

@app.route('/user/<user_name>/<int:user_id>')
def user(user_name, user_id):
    return f'Hello, {user_name}({user_id})!'

if __name__ == '__main__':
    app.run(debug=True)
```

## templates
