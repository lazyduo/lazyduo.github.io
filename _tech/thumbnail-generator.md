---
title: "Tech > Project LOLHUB > Thumbnail Generator"
layout: tag
taxonomy: thumbnail
classes: wide
author_profile: false
sidebar:
    nav: "tech"
---

원하는 스타일의 Youtube Thumbnail을 생성해주는 App 입니다. Python PIL 라이브러리로 Image Processing 했습니다. 비록 완전히 정해진 스타일 안에서만 만들 수 있다는 단점이 있지만, 채널 운영자라면 고정된 스타일을 만들어 놓고 사용하면 편리할 것 입니다. (물론 스타일을 코딩해야되는 것은 사용자 몫입니다)

- 예시

<figure class="half">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-sample-1.png">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-sample-2.png">
</figure>

이 페이지에서는 이 썸네일 생성기를 어떻게 만들었는지 그 과정을 다루도록 하겠습니다. 기억 되살리는 중...

## PIL 시작하기
