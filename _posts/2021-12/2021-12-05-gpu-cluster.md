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
    - 여러 모델 중 가장 적합한 모델 찾기.

2. Large scale distributed training
    - Quickly training a model
    - 엄청나게 많은 데이터셋을 한 모델에 훈련시키기.

3. Production inference
    - Deploying the model at scale to production
    - 서비스화 된 AI 모델을 사용자 요청에 따라 수행하기.