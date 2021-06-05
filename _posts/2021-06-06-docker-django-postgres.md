---
title: "Docker - Django & PostgreSQL"
date: 2021-06-06 01:33:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - docker
---

Django + PostgreSQL 프로젝트를 `dockerlize` 시키기 위한 여정...

## Dockerfile

`Dockerfile` 작성시 유의사항은, 파일명을 꼭 'Dockerfile'로 할 것! 그리고 WORKDIR 설정을 잘 해줘야 한다. Docker에서 기본 설정한 default path가 있어서 그것에 맞지 않으면 docker build 할 때 파일을 잘 찾지 못한다.

- Dockerfile

    ```dockerfile
    FROM python:3.9
    ENV PYTHONUNBUFFRED=1
    WORKDIR /code
    COPY . .
    RUN pip install -r requirements.txt
    ```

- requirements.txt

    ```
    Django==3.2.3
    django-crispy-forms==1.11.2
    Pillow==8.2.0
    psycopg2==2.8.6
    ```


## docker-compose.yml

docker compose를 이용하기 위해 `docker-compose.yml`을 아래와 같이 설정해준다.

이 때, django의 경우 `manage.py`를 이용해서 커맨드를 하므로, path 설정을 잘 해주어야한다. 어찌저찌 돌아가게끔 만들어는 놨는데, 'volume'에 대한 이해가 좀 필요할 것 같다.

Dockerfile에서 `COPY . .` 으로 Dockerfile과 동일한 directory에 있는 모든 파일을 'WORKDIR'인 './code'로 옮겨 놓았고, 내가 찾을 `manage.py`는 하위 디렉토리인 'lazydots'에 있으므로 아래 volume의 설정을 다음과 같이 하였다.

```yml
version: "3.9"

services:
    db:
        image: postgres
        volumes:
            - ./data/db:/var/lib/postgresql/data
        environment:
            - POSTGRES_DB=<DB_NAME>
            - POSTGRES_USER=<USER_NAME>
            - POSTGRES_PASSWORD=<USER_PASSWORD>

    web:
        build: .
        command: python manage.py runserver 0.0.0.0:8000
        volumes:
            - ./lazydots:/code
        ports:
            - "8000:8000"
        depends_on:
            - db
```

## Volumes

postgres의 path가 이상하다. 'migrate'를 해서 DB를 만들고 나서야 정상적으로 화면이 뜨긴 하는데, 기존에 'local'에서 작성한 DB 내용이 없다. path 설정을 확인 할 필요가 있어 보인다.

(아직 해결중)