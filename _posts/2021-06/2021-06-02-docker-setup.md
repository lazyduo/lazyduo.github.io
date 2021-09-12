---
title: "Docker 설치하기 for Windows 10"
date: 2021-06-02 21:42:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - docker
    - DevOps
---

`Docker`를 처음 써보려고 합니다. 역시나 설치가 만만치 않습니다. 그래도 docker가 가능하게 해줄 것들이 많기 때문에 꾹 참고 잘 설치해봅시다.

먼저, [docker hub](https://hub.docker.com/)에서 window용 설치파일을 다운 받습니다. 설치가 다 되고 `Docker Desktop`을 열면 아마 웬만하면 아래와 같은 에러들이 몇가지 뜰 겁니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/docker-setup01.PNG){: .align-center}

천천히 가이드를 따라가다 보면 충분히 해결할 수 있으니 겁먹지 맙시다.

먼저, 쉽게 확인 할 수 있는 부분은 '작업관리자 -> 성능'에서 `가상화`가 사용가능한지 확인합니다. Docker가 Virtual Machine과는 조금 다르지만 그래도 어느 정도 가상화를 사용하기 때문에 이 설정이 '가능'해야 되는 것 같습니다. '사용하지 않음'으로 되어 있다면, `BIOS`에서 가상화 설정이 되어있지 않을 확률이 높습니다. 컴퓨터를 재부팅 시켜서 BIOS 모드로 진입 하여 'CPU' 설정 부분을 잘 찾아서 가상화 항목을 'Enabled' 시킵니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/docker-setup00.PNG){: .align-center}

제 경우는, 가상화 설정이 끝나니 `Linux Kernel`을 설치하라고 떴고, 링크를 따라 업데이트 패키지를 다운 받고 재시작을 하니 최종적으로 무사히 `Docker Desktop`을 실행 할 수 있었습니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/docker-setup02.PNG){: .align-center}