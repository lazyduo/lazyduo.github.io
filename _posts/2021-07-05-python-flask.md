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

python 웹 프레임워크로 'django' 밖에 안써봐서 `flask`도 한 번 써보기로 했습니다.

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

우선 main 실행은 'app.run(debug=True)'으로 app.py를 실행시키면 server를 run 시켜 줍니다. 이 때, 'debug=True' 옵션은 'app.py'가 수정이 일어날 때 바로바로 반영 시켜서 보여주게끔 합니다. 테스트 용으로는 웬만해서는 'debug=True' 해주면 될 것 같습니다. django에서 manage.py가 전체적인 서버 런을 담당하는 것과 비교해서 간편해 보입니다.

`@app.route('/')`는 Flask class에서 준비된 함수가 트리거 되어 URL을 rendering 할 수 있도록 하는 decorator이다.

아래와 같이 기본 url에서 'Hello World'를 출력할 수 있게 끔 한다. 이 때 반드시 '/'로 시작해야하는 것을 주의 합니다.

url로 부터 변수를 사용하고 싶으면 아래 쪽의 `@app.route('/user/<user_name>/<int:user_id>')` 예시 처럼 사용하면 됩니다.

이제 `python app.py`로 서버를 실행 시키고 해당 주소로 들어가면, '/user/dada/30'에서 'Hello, dada(30)!'을 출력할 것입니다.

**Running on http://127.0.0.1:5000/**!!

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

`@app.route`에서 'index.html'과 같은 html을 rendering 할 수 있도록 해 봅니다. 우선 html 파일은 폴더 내에 `templates` 폴더를 만들고 해당 경로에 추가합니다. 이는 약속이므로 반드시 'templates'라는 이름의 폴더를 추가해 주어야 합니다.

그리고, html을 렌더링 하기 위해서는 'app.py'에서도 약간의 변화를 주어야 합니다. 여기서는 `render_template` 내장 함수를 사용합니다. 변수에 렌더링 할 html 파일 명과, 추가하고 싶은 변수들을 넣어주면 됩니다.

`return render_template('index.html', name='dada', context=context)`에서와 같이 'name='dada''처럼 변수를 지정해서 넣어 줄 수 도 있고, context 처럼 dictionary 형태로도 넘길 수 있습니다. 이 변수를 활용하는 방법은 하단 'index.html'을 참고하면 쉽게 알 수 있습니다.

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
@app.route('/home')
def home():
    context={
        'name': 'cera',
        'id': 1992,
    }
    return render_template('index.html', name='dada', context=context)

@app.route('/user/<user_name>/<int:user_id>')
def user(user_name, user_id):
    return f'Hello, {user_name}({user_id})!'

if __name__ == '__main__':
    app.run(debug=True)
```

- templates/index.html

```html
<!DOCTYPE html>
<html>
    <head>

    </head>
    <body>
        <h1>Main</h1>
        <p>{{ name }}</p>
        {% if name == 'dada' %}
            <p>Welcome Dada</p>
        {% endif %}
        <p>context : {{ context.name }}</p>
        <ul>
            {% for key, value in context.items() %}
                <li>{{ key }} : {{ value }}</li>
            {% endfor %}
        </ul>
    </body>
</html>
```


- 출력 결과

<hr>
<div>
    <h1>Main</h1>
    <p>dada</p>

        <p>Welcome Dada</p>

    <p>context : cera</p>
    <ul>

            <li>name : cera</li>

            <li>id : 1992</li>

    </ul>
</div>
<hr>

