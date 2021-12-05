---
title: "Building a GPU cluster"
date: 2021-12-05 15:15:00 +0900
classes: wide
toc: true
tags:
    - tech
    - AIML
    - gpu
---

AIML을 위한 GPU server rack 설계하기. 아래 영상 메모.

[Building a GPU cluster for AI (Lambda)](https://www.youtube.com/watch?v=rfu5FwncZ6s)

## Intro

왜 GPU 실물 서버가 필요한가? Cloud 서버의 비용적 한계.

## 사용하고자하는 ML의 종류 파악하기

아래의 각 방법마다 필요한 GPU 서버의 성격이 달라짐.

1. Hyperpaameter search
    - Finding the best model

2. Large scale distributed training
    - Quickly training a model

3. Production inference
    - Deploying the model at scale to production