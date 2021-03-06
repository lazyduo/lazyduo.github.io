---
title: "Tech > Project LOLHUB"
layout: tag
taxonomy: lolhub
classes: wide
author_profile: false
sidebar:
    nav: "tech"
---

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/lolhub-thumbnail.png){: .align-center}

- [Youtube Channel Link](https://www.youtube.com/channel/UCMKzq7ckZQGIuKDwQu6Ds8A/featured)
## 프로젝트 개요
- 기간 : 2020.09 ~ 2020.11
- 목표 : 게임 하이라이트 자동 생성 및 유튜브 업로드 자동화 웹 서비스
- 참여 : 썸네일 자동 생성, 유튜브 API 연결, Django 웹 등

    - [Thumbnail Generator](/tech/thumbnail-generator/)
    - [Youtube API](/tech/youtube-api/)
    - [Django](/tech/django/)

- flow 설명 :

    1. Crawling 할 프로 선수 들을 설정하고, 게임에서 Double Kill과 같은 `Event`가 일어난 구간들을 체크한다. 이 때, `Event` 별로 가중치를 두어 '재밌는' 경기를 찾는게 목표다.
    2. 위에서 찾은 `Event`를 작은 클립들로 녹화를 진행한다.
    3. 관리자는 녹화된 서브 클립들을 확인하고 **별점(rating)**을 부여한다. 흥미로운 영상일 수록 점수가 높으며, 이 점수에 따라서 알고리즘으로 영상들의 순서를 결정한다. 하이라이트 영상이 처음 부터 끝까지 흥미를 끌 수 있는 영상 퀄리티를 보장하기 위함이다.
    4. 최종 confirm으로 서브 클립들을 하나의 영상으로 편집한다. 지정한 인트로, 아웃트로 및 BGM도 같이 믹싱한다.
    5. 유튜브에 업로드하기 위해 title, subtitle, tag를 설정하고, Thumbnail을 제작한다.
    6. 최종 타겟 Youtube 채널에 업로드 한다.

## 주저리주저리

갑자기 개발자 할거라고 1-2주 코드카데미에서 python 튜토리얼하고, 자료구조랑 알고리즘, 코딩 문제 막 시작하고 있을 때 [upoque](https://github.com/upoque)가 하던 프로젝트에 중간 투입.

하나의 script안에서만 놀던 코딩 문제랑 달리, 폴더도 여러개, script도 여러개, 언어도 여러개여서 당황했었다. 더군다나 python은 물론이요, txt로만 input 하다가 json이라는 구조체도 처음 알게 되었고, Django한다고 어릴 때 메모장으로 한 번 씩 해본 html과 css, 그리고 jQuery를 통한 ajax, Youtube API 까지. 아, Git이라는 것도 처음 써봤다. 하나부터 열까지 모든게 새로운 경험이었다.

맨 처음에 썸네일 이미지 처리할려고 PIL이라는 라이브러리를 사용 했는데, 애초에 다른 라이브러리를 써본적없는 나는 docs 읽는 것만 해도 한 세월이었다. 그래도 결국 원하는 이미지 형태를 만들고, 이 기능을 또 GUI에 연결한다고 한 세월, 다시 Django로 서비스 하기 위해 연결한다고 한 세월, 또 Youtube API 한다고 한 세월... 반복이었다. 그래도 새롭게 뭔가 하는게 재밌어서 시간 가는 줄 모르고 퇴근하고 몇 시간 씩 작업했다.

다 만들어 놓고 관리가 잘 안돼서 흐지부지 잊혀져 버리고, 유튜브 채널도 잘 안 됐지만 그래도 생각보다 많은 것을 배웠던 프로젝트.