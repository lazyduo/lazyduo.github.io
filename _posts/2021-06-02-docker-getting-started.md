---
title: "Docker Getting-Started"
date: 2021-06-02 23:36:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - docker
---

`Docker` Getting Started!!

## 자주 쓰는 명령어 정리

- 실행

    - `-d` - run the container in detached mode (in the background)
    - `-p 80:80` - map port 80 of the host to port 80 in the container
    - `docker/getting-started` - the image to use

    붙여서 `-dp` 로 사용.

    ```
    docker run -dp 80:80 docker/getting-started
    ```

- build image

    - Dockerfile 생성
    
        ```
        FROM node:12-alpine
        RUN apk add --no-cache python g++ make
        WORKDIR /app
        COPY . .
        RUN yarn install --production
        CMD ["node", "src/index.js"]
        ```
    - build

        ```
        docker build -t getting-started .
        ```

        'getting-started'라는 tag를 붙여서 현재 경로에 빌드한다.

- 사용 중 / 중지 / 제거

    ```
    docker ps
    docker stop <the-container-id>
    docker rm <the-container-id>
    ```

    docker desktop에서 간단하게 바로 remove 시켜도 됨.

- docker hub

    ```
    docker tag getting-started lazyduo/getting-started
    docker push lazyduo/getting-started
    ```

    tagname default 값은 'latest'

- volume

    multi container가 DB등의 persist한 값을 참조하기 위한 형태

    - 생성

        ```
        docker volume create todo-db
        ```

    - run with volume

        `-v` 옵션으로 volume을 'mount'한다.

        ```
        docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
        ```


bind mount , docker compose는 좀 더 정리가 필요...