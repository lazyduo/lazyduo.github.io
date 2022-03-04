---
title: "Docker Local Registry"
date: 2022-03-04 13:17:00 +0900
classes: wide
toc: true
tags:
    - tech
    - ETC
    - docker
    - DevOps
---

Docker Hub를 통하지 않고 개인적으로 만든 Image를 `Docker Hub의 repository 처럼` 사용 하기 위해 하는 방법으로, **원래는 Docker Hub와 같은 repo 저장소인 registry를 사내에서 등 개인적으로 운영하기 위해 하는 방법이다.

> *(`registry` : repository들의 서버라고 보면 됨)*
> 

프로젝트 특화된 Image를 만들더라도 이를 이용해 Kubernetes Pods 세팅을 하기위해서는 Docker Hub와 같이 Public한 registry에서 부터 받아오게 해야하는데, 회사에서는 따로 Docker Registry를 운영하고 있지 않다. 따라서 이를 가능하게 하기 위해 필요한 Custom Image들을 `localhost:5000` registry로 올려서 사용한다.

reference → [link](https://docs.docker.com/registry/deploying/)

1. local 5000에 registry server를 daemon으로 실행시킨다.
    
    ```bash
    $ docker run -d -p 5000:5000 --restart=always --name registry registry:2
    ```
    
2. 원하는 이미지를 `localhost:5000/<image_name>`으로 새롭게 tag 한다.
    
    ```bash
    $ docker tag <origianl-name> localhost:5000/<image_name>
    ```
    
3. 만들어 놓은 local registry에 위 이미지를 push 한다.
    
    ```bash
    $ docker push localhost:5000/<image_name>
    ```
    
4. 확인
    
    필요 없는 기존 image 들을 삭제하고, local registry로 부터 pull 해본다.
    
    ```bash
    $ docker image remove <origianl-name>
    $ docker image remove localhost:5000/<image_name>
    
    $ docker pull localhost:5000/<image_name>
    ```
    
5. local registry 삭제 방법
    
    ```bash
    $ docker container stop registry # stop
    
    $ docker container rm -v registry # remove
    ```