---
title: "AWS Elastic Beanstalk - Django & PostgreSQL w/ Docker"
date: 2021-06-06 01:33:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - docker
    - aws
---

`Docker Compose` 된 Django + Postgres 프로젝트를 AWS의 `Elastic Beanstalk`로 배포하는 여정...

## Dockerfile 준비

Django + Postgres `Docker Compose`는 전에 다룬 내용이 있다.

## AWS Elastic Beanstalk

EB CLI 설치

[link](https://github.com/aws/aws-elastic-beanstalk-cli)

github를 통해서 설치한다.

git clone 후 setup.py가 있는 dir에서 `pip install .`

## EB Create