---
title: "Flask - CRUD Blog Tutorial"
date: 2021-07-10 13:00:00 +0900
classes: wide
toc: true
tags:
    - tech
    - language
    - python
    - flask
    - CRUD
---

Flask 공식 Tutorial을 통해 'Flaskr' 이란 이름의 기본적인 blog application을 만들었습니다. 해당 코딩 과정에서 기억해 두고 싶은 기법들을 개인 용도로 정리하였습니다.

[Flask Tutorial](https://flask.palletsprojects.com/en/2.0.x/tutorial/)

## Blueprint

`Blueprint`는 공통으로 사용하는 'view'들을 카테고리 별로 그룹화하여 관리하는 기법이라고 볼 수 있다.

```python
# flaskr/auth.py
from flask import Blueprint

bp = Blueprint('auth', __name__, url_prefix='/auth')

# flaskr/__init__.py
def create_app():
    app = ...
    # existing code omitted

    from . import auth
    app.register_blueprint(auth.bp)

    return app
```

## handling DB

'Flask'에서는 기본적으로 python 내장 DB인 `sqlite3`를 사용할 수 있다. DB 다루기가 익숙치 않아 명령어들을 몇 개 메모해두었다.

db의 'user' Table로 부터 찾고자 하는 username의 row를 한 개(`fetchone()`) 가져오기. 아래돠 같이 '?'를 사용하여 변수를 넣어 줄 수 있다.

```python
username = 'dada'
user _id= db.execute(
    'SELECT id FROM user WHERE username = ?', (username,)
).fetchone()

if user_id is not None:
    ...
    # omitted

```

JOIN 사용하기

```python
post = get_db().execute(
        'SELECT p.id, title, body, created, author_id, username'
        ' FROM post p JOIN user u ON p.author_id = u.id'
        ' WHERE p.id = ?'
        (id,)
    ).fetchone()
```

## redirect, url_for

flask에서 간편하게 `url_for()`를 사용하여 '이름'으로 url을 리턴하는데, 'auth.py'에 있는 login view는 아래처럼 표현한다.

```python
if request.method == 'POST':
    ...

    return redirect(url_for('auth.login'))
```

## login required

이 부분은 그냥 외워야 할 것 같다...

```python
import functools

def login_required(view):
    @functools.wraps(view)
    def wrapped_view(**kwargs):
        if g.user is None:
            return redirect(url_for('auth.login'))
        
        return view(**kwargs)
    
    return wrapped_view
```