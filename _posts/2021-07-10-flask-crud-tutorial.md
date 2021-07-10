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
