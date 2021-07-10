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

Flask 공식 Tutorial을 통해 'Flaskr' 이란 이름의 기본적인 blog application을 만들었습니다.

[Flask Tutorial](https://flask.palletsprojects.com/en/2.0.x/tutorial/)

## Blueprint

```python
from flask import Blueprint

bp = Blueprint('auth', __name__, url_prefix='/auth')
```
