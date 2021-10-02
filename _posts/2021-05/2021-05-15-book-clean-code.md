---
title: "[책] Clean Code - Robert C. Martin"
date: 2021-05-15 21:25:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - ETC_Posts
    - book
---

깊이 반성하고 코드 정리하러 갑니다.

어떤 코드가 좋은 코드인가? 가독성이 좋은 코드. python이 사람이 읽는 방식대로 읽히기 때문에 쉽다(?)고 알려진 것과 비슷한 맥락인 것 같다. 하지만, 프로그래밍 언어 자체가 가독성이 좋은 것과 **'가독성이 좋게 프로그래밍하는 것'**은 전적으로 프로그래머한테 달려 있다! (아차 싶었다)

## 이름과 함수

개인적인 생각으로는 **이름** 설정이 정말 어려운 것 같다. 영어 어휘가 부족해서 그럴 수도 있는데, 솔직히 핑계인 것 같고 이 skill을 기르려면 '잘 짰다고' 하는 스크립트를 보면서 배울 수밖에 없는 것 같다. 프로그래머들 사이에서 알려진 전통적인(?) rule을 따르는 것도 좋다. 분명 고심하면서 생긴 rule일 테니까. 더 좋은 것은 주변에 '잘 짜는' 사람이 있다면 정말 땡큐인듯 하다. 

## 주석

필요 없는 주석을 줄이자. 주석은 스크립트를 따라가지 못한다는 말에 백번 공감했다. 다른 함수에 영향을 주는 코드가 수정되었거나 하면 '에러'가 발생하기 때문에 저절로 함께 고치게 되어 있다. 하지만 주석은 그 변화를 자동으로 따라가지 못하므로 예전의 주석이 남겨져서 혼란을 줄 수 있다.

<br>
<br>

쓱 읽어서 이 코드가 무엇을 하는 것인지 알 수 있도록 하자!

'저자(author)'가 되어 '독자'에게 잘 읽히는 코드를 선사하자!