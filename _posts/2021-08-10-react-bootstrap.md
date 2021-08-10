---
title: "React - Bootstrap - Reactstrap"
date: 2021-08-10 08:59:00 +0900
classes: wide
tags:
    - tech
    - yumi
    - react
    - memo
    - web design
---

`YUMI Project`를 시작할 때는 Django를 더 많이 쓰겠지 했는데, 우리가 `React`를 활용한 Front End 작업을 맨땅에 헤딩하다 보니 새롭게 접하는 것들이 많았습니다.

이번에는 `Redux`나 `Hooks` 같이 기술적인 부분이 아니라 오로지 '디자인'적인 부분에 관해 살펴봅니다.

# 들어가기 앞서
## Sass (scss)

`Sass(Syntatically awesome stylesheets)` 기존의 'css'의 단점을 보완한 스크립트 언어이다. 프로젝트가 커짐에 따라 스타일 시트도 관리가 필요해지는데, 관리하는데 있어 매우 유용한 variable, nesting, mixini, inheritance 등의 개념이 추가 되었다. 이 sass는 기존의 css와는 문법이 약간 다른데, css와 완전히 호환되도록 새로운 구문을 도입한 것이 `scss`라고 한다. 요즘 프로젝트에서는 sass를 쓰기 위해 전부 `.scss`를 사용하는 것으로 보인다.

`scss`에서는 우리 프로젝트 structure에서 'src > assets > scss' 에서 확인할 수 있듯이 꽤나 심플하게 관리되고 있음을 알 수 있다. '.scss'는 약속으로 파일명에 `_` 언더바를 붙여서 쉽게 import한다.

```scss
@import "/scss/variables";
```

위 처럼 import를 하면 scss 디렉토리 하위의 '\_variables.scss' 파일을 자동으로 인식하게 된다.

보통의 scss를 사용하는 프로젝트들은 이렇게 'variables' 파일을 따로 두어 '\$'로 구분 하는 변수들을 전부 설정하여 모든 스타일 시트에 쉽게 적용할 수 있도록 사용하는 것으로 보인다.

```scss
// _variables.scss

$header-height: 70px;
$header-bg: #ffffff;
$header-item-color: #555b6d;
```

(header 관련된 변수들을 설정한 모습)

## Bootstrap?
