---
title: "Ubuntu GUI & Remote Control"
date: 2022-01-19 14:09:00 +0900
classes: wide
tags:
    - ETC
    - ETC_Posts
    - DevOps
---

NVIDIA 온라인 자율학습 강의 수강 중에 학습 형태가 괜찮은 것 같아서 글을 남긴다.

기본 적으로 EC2 위에서 돌아가는 Jupyter Notebook 환경에서 학습 환경을 쭉 따라서 하게끔 만들어 놨고,

중간 중간에 직접 파일들을 수정하면서 output을 확인하는 형태였음.

그 중에서도 Nsight Systems를 익히기 위해 Remote Desktop을 열어서 학습하는 부분이 있었는데 이게 좀 신기했음.

### Ubuntu Desktop(GUI)

NVIDIA에서 사용한 GUI는 `Xfce Desktop`이었다.

굉장히 lightweight라는 특징을 가지고 있어 이러한 학습용으로 slim하게 설치하는데 유리한 듯.

```bash
$ sudo apt-get install xfce4 slim
$ sudo services slim start
```

### noVNC

Javascript Library로 `Virtual Network Computing`를 웹 브라우저에서 가능하게 해준다!!

NVIDIA가 이 `noVNC`를 활용하여 AWS EC2에 올라가 있는 학습 인스턴스를 웹 브라우저로 원격 접속을 가능하게 해주었다.


아무튼 이렇게 서비스 할 수 도 있다라는 점...메모...
