---
title: "Tech > AI/ML > TensorFlow"
layout: tag
taxonomy: tensorflow
classes: wide
author_profile: false
sidebar:
    nav: "tech"
tag:
    - AIML
---
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/tensorflow.png){: .align-center}

## TensorFlow?

Google Brain team에서 개발한 머신러닝 프레임워크. Python Friendly하게 만들어져 일반인들도 사용하기 쉬운(?)편이다. 아직까지는 다른 프레임워크들과 대비해 커뮤니티가 활발하고 자료가 많아 간단하게 개발하는데 있어서는 사용자가 많아 유용하다.

Facebook's AI Research lab에서 개발한 **PyTorch**와 가장 큰 차이점은 고정된 신경망이냐 레이어 구조의 신경망이냐의 차이인데, 레이어 구조를 사용하는 **PyTorch**가 더 최적의 학습효과를 보여준다. 하지만, 큰 프로젝트나 복잡한 workflow에서는 **TensorFlow**가 더 뛰어난 퍼포먼스를 보여준다고 한다.

또 다른 머신러닝 프레임워크들로는 neural network에 특화된 마이크로소프트의 **CNTK**, 그리고 Amazon의 **Apache MXNet** 등이 있다.

## Tensor?

Machine Learning에서 Data가 Neural Network를 타고 들어갈때의 단위라고 보면 된다. 배열이나 행렬 정도로 느낌을 가져가면 '우선'은 이해가 편하다. 결국 Machine Learning이란게 Data들에 **가중치**를 부여하면서 선형결합을 하여 다음 노드(node)를 만들고 또 다음 층(layer)으로 선형결합을 하며 이루어지는데 이게 결국 `tensor`의 연산이다.

너무 수학적 혹은 물리적으로 갈 것 까지는 없고, 1차원 벡터, 2차원 매트릭스 3차원 부터 텐서라고 한다고 생각하면 편하다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/tensor.png){: .align-center}

## Tutorial

TensorFlow 사이트에 잘 정리된 [튜토리얼](https://www.tensorflow.org/tutorials/keras/classification?hl=en)이 있습니다. 같은 구글이라서 전에 Youtube API 문서 들여다 봤던 거랑 느낌이 아주 유사네요.

차근차근 포스팅 할 예정입니다.