---
title: "Tech > Project LOLHUB > Youtube API"
classes: wide
author_profile: false
toc: true
sidebar:
    nav: "tech"
---

## 개요

LOLHUB 프로젝트의 최종 단계는 클릭 한 번으로 자동으로 Youtube <span><i class="fa fa-youtube"></i></span>에 업로드 하는 것 까지 였습니다. 이 글에서는 Youtube Access 권한을 얻고, 동영상 업로드를 위한 설정을 세팅 한 후에, 핸들러와 크롬 드라이브를 통한 자동 업로드까지 다뤄보도록 하겠습니다.

## OAuth Protocol
 
Youtube API를 사용하기 위해서는 OAuth 인증이 필수다.

Youtube에서 업로드까지 당연히 API를 제공하지만, quote 인증 문제도 있고 해서 `Selenium`으로 임시 구현했습니다.


