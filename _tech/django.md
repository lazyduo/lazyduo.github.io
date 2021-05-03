---
title: "Tech > Project LOLHUB > Django"
classes: wide
author_profile: false
toc: true
sidebar:
    nav: "tech"
---

LOLHUB Project에서는 웹으로 App을 사용하기 위해 Python 특화 웹 프레임워크인 Django를 사용했다. 처음에는 로컬에서 `PYQT`로 GUI 짜서 버튼에다가 모델 엮어서 사용하다가 **Web**에서 사용가능하게끔 하기 위해 Django로 서비스를 만든 것이다. 상용 프로그램은 아니었고 개인 채널을 위해 만든거라 이렇게까지 하나 싶었지만, 그래도 server만 돌고 있다면 `폰`으로도 제작된 영상 확인하고 썸네일 만들고 유튜브에 올릴 수 있다는게 진짜 큰 장점이었다.

여튼! 지금은 연결이 다 망가져서 다시 돌리기는 조금 힘들지만, 그래도 Django로 구축하느라 python도 모잘라 JS랑 html/css도 했으니 좋은 경험이었던 것은 분명하다. Python 2주 대충 인터넷에서 배우다가 프로젝트 개발에 뛰어들어서 이걸 했냈다는거 사실만으로도 나름(?) 대단했다고 생각한다.

그 때는 왜 하는지도 잘 몰랐고 이해 못하고 넘어가는 것들이 많았는데 다시 정리하면서 기억을 늦게나마 되살려 보자.

## Django?

[사이트](https://www.djangoproject.com/) 가 보면,

>Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design.

이라고 되어 있다. 그렇다. Python 특화 **Web Framework**다. 웹 프레임워크는 웹 App 등을 개발 할 때 사용하는 DIY 키트라고 보면 된다. 공통적인 기능들은 매번 다시 개발하거나 하면 시간 낭비이고, 웹을 구현할려면 그쪽 전문 개발인력이 따로 붙어야된다.

이를 방지하기 위해 어느정도 틀(Frame)을 잡아 놔서 main 개발에만 집중 할 수 있도록 해주는 '뼈대와 클래스, 라이브러리를 포함하는 Tool' 정도로 보면 될 것 같다.

Python의 경우 Django 웹 프레임워크가 가장 널리 알려졌고, Java의 Spring, Node.js의 Express, Ruby의 Ruby on Rails등이 알려져 있다.

## MVC vs MVT 패턴

Django를 이해하기 위해서 흔히 얘기하는 MVC 패턴과 비교하면 좋다. Django는 이 MVC(Model, View, Controller) 패턴과는 사뭇 다른 MVT(Model, View, Template) 패턴을 사용하기 때문이다.

사실 지금까지 MVC 패턴이 뭔지도 몰랐는데 다른 포스트에서 '한 번 쯤'들어 봤을 거라고 해서 굉장히 당혹스러웠다. 아무튼 웹 개발에서 흔히 사용되는 디자인 패턴인 MVC 패턴은 
