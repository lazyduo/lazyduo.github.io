---
title: "Suvervised and Unsupervised learning"
date: 2021-11-07 18:32:00 +0900
classes: wide
toc: true
tags:
    - tech
    - AIML
---

`Supervised Learning`과 `Unsupervised Learning` 기본 개념 정리.

## Supervised Learning

`Labeled` 데이터로 학습하는 것을 의미한다. 단어 의미에서도 알 수 있듯이 감독해주는 '선생님'이 있어서 특정 데이터가 A인지 B인지 알려주면서 학습하게된다.

- Types
    - Regression
    - Logistic Regression
    - Classification
    - Naive Bayes Classifiers
    - K-NN (k nearest neighbors)
    - Decision Trees
    - Support Vector Machine

- Disadvantages
    - 빅데이터를 분류하는데 있어서 다소 챌린징하다.
    - 트레이닝을 하는데 소요되는 시간이 상당히 큰 편 이다.

## Unsupervised Learning

지도 학습(Supervised Learning)과는 달리 데이터 셋이 어떤 것인지 가이드가 없다. 즉, `Unlabeled` 데이터를 가지고 학습하여 알아서 'clustering'을 한다. 특정 cluster가 정확히 어떤 것인지는 모르지만 비슷한 특징을 가진 데이터들을 묶는다.

비지도 학습(Unsupervised Learning)은 크게 두가지로 분류된다.

- Clustering: data 안에서 특징 별로 그룹핑을 하고 싶을 때. 고객들의 소비 패턴 별로 나누고 싶을 때.
- Association: data 들의 상관 관계를 밝혀 내고 싶을 때. X를 사는 사람은 Y도 사더라.

## 참고

[Link](https://www.geeksforgeeks.org/supervised-unsupervised-learning/)